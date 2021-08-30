<template>
  <div class="first">
    <div class="second" v-if="show">
      <h1>{{prop}}</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    prop: String,
    show: Boolean
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .first {
    display: flex;
    height: 25vw;
    width: 25vw;
    border: 1px solid gray;
    border-radius: 4vw;
    flex-direction: row;
    align-items: center;
  }
  .second {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  h1 {
    font-size: 15vw;
    text-align: center;
  }
  @media only screen and (min-width: 800px) {
  .first {
    height: 10vw;
    width: 10vw;
    border-radius: 2.4vw;
  }
  h1 {
    font-size: 6.2vw;
    text-align: center;
  }
}
</style>
