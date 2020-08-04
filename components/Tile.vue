<template>
<div class="tile" @click="check()" @contextmenu="flag($event)" :class="{red:TileType === 1}" >
  <div class="content">
{{TileScore}}
  </div>
</div>
</template>

<script lang="ts">
    import Vue from "vue";
    export default Vue.extend({
        name: "Tile",
      data(){
          return{
           showing: false
          }
      },
      props: {
        TileType:{
          type: Number
        },
        TileIndex:{
          type: Number
        },
        TileScore:{
          type: Number
        }
      },
      methods:{
          check:function () {
            this.showing = true
            this.$emit('check', this.TileIndex, this.TileType)
          },
        flag: function (e:any) {
        this.showing = true
        e.preventDefault();
        }
      },
      mounted() {
          this.check()
      }
    })
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
.red{
  background: red;
}
</style>
