<template>
<div id="bord" @contextmenu="no($event)">
  <Tile v-for="tile in 100"></Tile>
</div>
</template>

<script>
    import Tile from "./Tile";
    export default {
        name: "Bord",
      components: {Tile},
      methods:{
          no:function (e) {
            e.preventDefault()
          }
      }
    }
</script>

<style scoped>
#bord{
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(10, 1fr);
  grid-gap: 1vw;
  padding: 1vw;
  box-sizing: border-box;
  height: 40vw;
  width: 40vw;
  background: tan;
}
</style>
