<template lang="pug">
  q-page(padding)
    .text-h8(v-if="!winning && !loosing") {{ $t('aladin_note') }}
    .text-h3(v-if="winning") {{$t('you_win!')}}
    .text-h3(v-if="loosing") {{$t('you_loose!')}}
    .q-pa-md
      .row
        .col-12
          q-select(v-model="cards", :label="$t('cards')", @input="reset", :options="[10, 15, 20, 25, 30]")
      .row
        .col-3
          .text-h6 {{ $t('aladins') }}
        .col-3
          .text-h6 {{ $t('total') }} {{sum(aladins)}}
        .col-3(v-for = "a in aladins")
          q-btn(color="green") {{a}}
      .row
        .col-3
          .text-h6 {{ $t('jafars') }}
        .col-3
          .text-h6 {{ $t('total') }} {{sum(jafars)}}
        .col-3(v-for = "j in jafars")
          q-btn(color="blue") {{j}}
      .row
        .col-3(v-for = "n in myCards")
          q-btn(size = "lg"  v-bind:style = "{ 'background-color': hasFactor(n) ? rgb : 'red'}" @click = "take(n)") {{n}}
</template>

<script>
export default {
  name: 'Aladin',
  props: ['rgb'],
  data () {
    return {
      winning: false,
      loosing: false,
      cards: 10,
      myCards: [
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10
      ],
      aladins: [],
      jafars: []
    }
  },
  methods: {
    reset: function () {
      this.winning = false
      this.loosing = false
      this.myCards = []
      for (var i = 1; i <= this.cards; i++) {
        this.myCards.push(i)
      }
      this.aladins = []
      this.jafars = []
      this.$forceUpdate()
    },
    hasFactor: function (n) {
      var factors = this.myCards.filter((o) => { return n % o === 0 })
      return factors.length > 1
    },
    take: function (n) {
      var factors = this.myCards.filter((o) => { return n % o === 0 })
      if (factors.length > 1) {
        this.aladins.push(n)
        this.remove(n)
        for (var i = 0; i < factors.length - 1; i++) {
          this.jafars.push(factors[i])
          this.remove(factors[i])
        }
      } else {
        this.jafars.push(n)
        this.remove(n)
      }
      this.check()
    },
    remove: function (n) {
      this.myCards = this.myCards.filter((o) => { return o !== n })
      this.$forceUpdate()
    },
    sum: function (list) {
      var ans = 0
      for (var i = 0; i < list.length; i++) {
        ans += list[i]
      }
      return ans
    },
    check: function () {
      if (this.myCards.length === 0) {
        if (this.sum(this.aladins) > this.sum(this.jafars)) {
          this.winning = true
          setTimeout(this.reset, 2000)
        } else {
          this.loosing = true
          setTimeout(this.reset, 2000)
        }
      }
    }
  }
}
</script>

<style>

.text-h8 {
  font-size: 16px;
  white-space: pre-wrap;
}
</style>
