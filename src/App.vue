<template>
  <div id="app">
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }

  #app {
    width: 100vw;
    height: 100vh;
    background: linear-gradient(to bottom right, #83C0B9 70%, #B8A5D9);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  @media (max-height: 400px) {
    #app {
      width: 100%;
      height: 100%;
    }
  }

</style>
