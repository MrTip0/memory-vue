<template>
  <div class="board">
    <card v-for="(prop, index) in list" :key="index" :prop="prop.value" :show="prop.show" @click="show(index)"/>
  </div>
</template>

<script>
import Card from './components/Card.vue'

export default {
  data() {
    return({
      list: [],
      actual: null,
      opened: []
    })
  },
  created() {
    let select = ['❤️', '💵', '🔮', '👻', '😀', '🧠', '❤️', '💵', '🔮', '👻', '😀', '🧠']
    for (let i = 0; i < 12; i++) {
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
  methods:{
    show(index){
      if (!this.opened.includes(index) && this.actual != index && this.list[index].show == false) {
        this.list[index].show = true
        if (this.actual == null) {
          this.actual = index
        } else {
          if (this.list[index].value == this.list[this.actual].value) {
            this.opened.push(index)
            this.opened.push(this.actual)
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
  name: 'App',
  components: {
    Card
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.board {
  display: grid;
  grid-template-columns: 25vw 25vw 25vw;
  grid-template-rows: auto;
  gap: 2vw 2vw;
}
</style>
