<template>
  <div id="app">
    <div class="main-container">
      <CryptoList />
    </div>
  </div>
</template>

<script>
  import CryptoList from "./components/CryptoList";

  export default {
    name: 'App',

    components: {
      CryptoList,
    }
  }
</script>

<style lang="scss">
 * {
   box-sizing: border-box;
 }

  body {
    background-color: #d4e4ec;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #475c70;
    margin: 40px 140px;

  }
</style>
