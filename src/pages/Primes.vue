<template lang="pug">
  q-page(padding)
    q-btn(color = "green" @click = "start(); stop = false") {{$t('start')}}
    q-btn(color = "red" @click = "stop = true") {{$t('stop')}}
    .text-h6 {{$t('step')}}{{step}}
    .q-pa-md
       .row
        .col-4 {{$t('primes')}}
        .col-8(v-if = "step != 5")
          .text-h6 {{primes.slice(0,step)}}
        .col-8(v-if = "step == 5")
          .text-h6 {{primes}}
       .row(v-for = "i in [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]")
        .col(v-for = "j in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]")
          a(@click = "makeColor(i+j)" v-bind:style="{ 'background-color': isPrime(i+j) ? rgb : 'white'} " v-bind:class = "{ 'color' : (i+j) % myNum == 0, 'color1' : i+j == 1, 'color2' : (i+j) % 2 == 0 && i+j != 2 && step > 0, 'color3' : (i+j) % 3 == 0 && i+j != 3 && step > 1, 'color5' : (i+j) % 5 == 0 && i+j != 5 && step > 2, 'color7' : (i+j) % 7 == 0 && i+j != 7 && step > 3, 'small': i+j == 100}") {{ i+j }}

</template>

<script>
export default {
  name: 'Primes',
  props: ['rgb'],
  data () {
    return {
      myNum: 1000,
      stop: false,
      step: 0,
      primes: [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 77, 79, 83, 89, 97],
      interval: undefined
    }
  },
  methods: {
    isPrime (n) {
      if (this.step < 5) {
        return this.primes.slice(0, this.step).indexOf(n) > -1
      } else {
        return this.primes.indexOf(n) > -1
      }
    },
    makeColor (n) {
      this.myNum = n
    },
    go () {
      if (!this.stop) {
        this.step++
        this.step = this.step % 6
      }
    },
    start () {
      clearInterval(this.interval)
      this.interval = setInterval(this.go, 3000)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.row {
  padding: 0 !important;
}

.col {
  text-align: right;
  padding: 0 !important;
  overflow: hidden;
  width: 8vw;
}

a {
  color: black;
  font-size: 22px;
  display: inline-block;
  min-width: 6vw !important;
  width: 100%;
  padding: 6px 2px;
  border: 1px black solid;
  transition: all 0.8s ease;
}

a.color {
  background-color: #af0 !important;
}

a.color1 {
  background-color: #999 !important;
}

a.color2 {
  background-color: #c03 !important;
}

a.color3 {
  background-color: #f00 !important;
}

a.color5 {
  background-color: #c30 !important;
}

a.color7 {
  background-color: #a00 !important;
}

.small {
  font-size: 16px;
  line-height: 2.1;
}
</style>
