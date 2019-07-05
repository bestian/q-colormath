<template lang = "pug">
  q-page(padding)
    q-toolbar
      q-toolbar-title
        span(v-if = "myNum == 1000") 點擊任意數字，看看它的所有倍數
        span.bold(v-if = "myNum !== 1000") {{myNum}}的倍數
    .q-pa-md
      .row(v-for = "i in [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]")
        .col(v-for = "j in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]")
          a(@click = "makeColor(i+j)" v-bind:style = "{ 'background-color' : (i+j) % myNum == 0 ? rgb : 'white'}" v-bind:class = "{ 'color' : (i+j) % myNum == 0, 'small': i+j == 100}") {{i + j}}
</template>

<script>
export default {
  name: 'M_Color',
  props: ['rgb'],
  data () {
    return {
      myNum: 1000
    }
  },
  methods: {
    makeColor (n) {
      this.myNum = n
    }
  }
}
</script>

<style>
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
  color: #39c;
  font-size: 22px;
  display: inline-block;
  min-width: 6vw !important;
  width: 100%;
  padding: 6px 2px;
  border: 1px black solid;
  transition: all .8s ease;
}

.color {
  background-color: #af0;
}

.small {
  font-size: 16px;
  line-height: 2.1;
}

.bold {
  font-weight: bold;
}

</style>
