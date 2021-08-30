<template>
  <div class="board">
    <card v-for="(prop, index) in list" :key="index" :prop="prop.value" :show="prop.show" @click="show(index)"/>
  </div>
</template>

<script>
import Card from './Card.vue'

export default {
  data() {
    return({
      list: [],
      actual: null,
      opened: [],
      todo: 0,
      done: 0
    })
  },
  created() {
    this.configGame()
  },
  methods:{
    configGame() {
      this.opened = []
      this.actual= null,
      this.todo = this.items.length
      this.done = 0
      let select = this.items.concat(this.items)
      let l = select.length
      this.list = []
      for (let i = 0; i < l; i++) {
        let value = Math.floor(Math.random() * select.length);
        this.list.push({
          value: select[value],
          show: false
        })
        let temp = select[value]
        select[value] = select[select.length - 1]
        select[select.length - 1] = temp
        select.pop()
      }
    },
    show(index){
      if (!this.opened.includes(index) && this.actual != index && this.list[index].show == false) {
        this.list[index].show = true
        if (this.actual == null) {
          this.actual = index
        } else {
          if (this.list[index].value == this.list[this.actual].value) {
            this.opened.push(index)
            this.opened.push(this.actual)
            this.done ++
            if (this.done == this.todo) {
              this.$emit('endedgame')
            }
          } else {
            let def = this.actual
            setTimeout(()=>{
              this.list[index].show = false
              this.list[def].show = false
            }, 500)
          }
          this.actual = null
        }
      }
    }
  },
  name: 'GameBoard',
  components: {
    Card
  },
  props: {
    items: Array,
  },
  watch: {
    items: function() {
      this.configGame()
    }
  }
}
</script>

<style>
.board {
  display: grid;
  grid-template-columns: 25vw 25vw 25vw;
  grid-template-rows: auto;
  gap: 2vw 2vw;
}
@media only screen and (min-width: 800px) {
  .board {
    grid-template-columns: 10vw 10vw 10vw 10vw 10vw 10vw;
  }
}
</style>
