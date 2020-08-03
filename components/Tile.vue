<template>
<div class="tile" @click="check()" @contextmenu="flag($event)">
  <div class="content" v-if="showing">
{{TileType}}
  </div>
</div>
</template>

<script>
    export default {
        name: "Tile",
      data(){
          return{
           showing: false
          }
      },
      props: {
        TileType:{
          type: String
        },
      },
      methods:{
          check:function () {
            this.showing = true
          },
        flag: function (e) {
        this.showing = true
        e.preventDefault();
        }
      }
    }
</script>

<style scoped>
.tile{
  border: white 3px solid;
  display: grid;
  align-items: center;
  justify-items: center;
  height: 2vw;
  width: 2vw;
  box-sizing: border-box;
}
</style>
