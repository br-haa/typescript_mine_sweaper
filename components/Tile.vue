<template>
<div class="tile" @click="check()" @contextmenu="flag($event)">
  <div class="content">
{{showing}}
  </div>
</div>
</template>

<script>
    export default {
        name: "Tile",
      data(){
          return{
           showing: 0
          }
      },
      methods:{
          check:function () {
            this.showing = 1
          },
        flag: function (e) {
        this.showing = 2
        e.preventDefault();
        }
      }
    }
</script>

<style scoped>
.tile{
  border: white 3px solid;
}
</style>
