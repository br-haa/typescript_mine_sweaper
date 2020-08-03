<template>
<div id="bord" @contextmenu="no($event)" :style="{gridTemplateColumns: `repeat(${PropAmount*5}, 1fr)`, gridTemplateRows: `repeat(${PropAmount*5}, 1fr)`}">
  <Tile v-for="tile in items" :tile-type='tile.id'></Tile>
</div>
</template>

<script lang="ts">
    import Vue from 'vue'
    import Tile from "./Tile";
    export default Vue.extend({
      name: "Bord",
      components: {Tile},
      data (){
        return{
          amount: 100,
          difficulty: 20,
          items: [] as Object[]
        }
      },
      props:{
        PropAmount:{
          type: Number,
          default: 1
        }
      },
      methods:{
        getAmount: function (){
        this.amount = this.PropAmount * 5
          this.amount = this.amount * this.amount
        },
          no:function (e:any) {
            e.preventDefault()
          },
        setUp: function (){
          this.getAmount()
          this.addBombs()
          this.addRest()
          this.shuffleArray(this.items)
        },
        addBombs: function (){
            interface T {
              id: number;
              name: string;
            }
            for(let i = 0; i < (100 / this.amount) * this.difficulty; i++){
              let oob: T = {id: 1, name: 'bomb'}
              this.items.push(oob)
            }
        },
        addRest: function (){
            interface T {
              id: number;
              name: string;
            }
          for(let i = 0; i < this.amount - (100 / this.amount) * this.difficulty; i++){
            let oob: T = {id: 0, name: 'neutral'}
            this.items.push(oob)
          }
        },
        shuffleArray: function (array: Object[]) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
    }
      },
      mounted(){
        this.setUp()
      }
    })
</script>

<style scoped>
#bord{
  display: grid;
  grid-gap: .3vw;
  padding: .3vw;
  box-sizing: border-box;
  background: tan;
}
</style>
