<template>
    <form v-if="!started" @submit.prevent="restart()">
        <input type="text" v-model="value">
        <input type="submit" value="start">
    </form>
    <GameBoard :items="items" v-if="show" @endedgame="ended()"/>
</template>

<script>
import GameBoard from './components/GameBoard.vue'

export default {
    data() {
        return({
            items: ['❤️', '💵', '🔮', '👻', '😀', '🧠'],
            value: "❤️, 💵, 🔮, 👻, 😀, 🧠",
            started: false,
            show: false
        })
    },
    name: 'App',
    components: {
        GameBoard
    },
    methods: {
        changeItems(){
            this.items = this.value.replace(/\s+/g, '').split(',')
        },
        restart() {
            this.started = true
            this.show = true
            this.changeItems()
        },
        ended() {
            this.started = false
        }
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
</style>

<style scoped>
input {
    height: 4vw;
    margin: 1vh;
    font-size: 3vw;
    background: none;
    border: 1px solid gray;
    text-align: center;
    border-radius: 0.5vw;
    text-transform: uppercase;
}
</style>