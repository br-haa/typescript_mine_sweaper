<template>
  <div id="pageHolder">
    <Nuxt />
    <Bord></Bord>
  </div>
</template>

<script>
  import Bord from "../components/Bord";
  export default {
    components: {Bord}
  }
</script>

<style>
  #pageHolder{
    display: grid;
    align-items: center;
    justify-items: center;
    height: 98vh;
  }
</style>
