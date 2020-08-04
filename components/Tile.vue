<template>
<div class="tile" @click="check()" @contextmenu="flagSet($event)"
     :class="{pressed:showing === true, red:TileType === 1 && showing === true, neutral:showing === false}" >
  <div class="content" v-if="showing">
{{TileScore}}
  </div>
  <div class="flag" v-if="showing === false && flag === true">

  </div>
</div>
</template>

<script lang="ts">
    import Vue from "vue";
    export default Vue.extend({
        name: "Tile",
      data(){
          return{
           showing: false,
            flag: false
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
        flagSet: function (e:any) {
        this.flag = true
        e.preventDefault();
        }
      }
    })
</script>

<style scoped lang="scss">
.tile{
  background: linear-gradient( to bottom right, white, #efefef);
  box-shadow: -2px -2px 5px #ffffff, 2px 2px 5px #000000;
  display: grid;
  align-items: center;
  justify-items: center;
  height: 2vw;
  width: 2vw;
  box-sizing: border-box;
  cursor: pointer;
  transition: .3s ease-in-out;
  border-radius: 3px;
  overflow: hidden;
}
.neutral{
  &:hover{
    box-shadow: -1px -1px 4px #eeeeee, 2px 2px 6px #4f4f4f;
    transform: scale(1.1);
  }
}
.red{
  background: red !important;
}
.pressed{
  background: linear-gradient( to bottom right, white, #efefef);
  box-shadow: -2px -2px 5px #ffffff inset, 2px 2px 5px #000000 inset;
}
.flag{
  background: yellow;
  height: 100%;
  width: 100%;
}
</style>
