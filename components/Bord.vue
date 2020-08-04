<template>
<div id="bord" @contextmenu="no($event)"
     :style="{gridTemplateColumns: `repeat(${multiplier}, 1fr)`, gridTemplateRows: `repeat(${multiplier}, 1fr)`}">
  <Tile v-for="(tile, index) in items" :tile-type='tile.id' :tile-index="index" :tile-score="tile.score" @check="test"></Tile>
</div>
</template>

<script lang="ts">
    import Vue from 'vue'
    import Tile from "./Tile.vue";
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
      computed: {
        multiplier(): number{
          return this.PropAmount * 10
        }
      },
      methods:{
        test: function (clickedIndex:number, type:number){
          if(type === 1){
          }else {
           this.score(clickedIndex)
          }
        },
        score: function (ci:number){
            let TL = this.items[ci- (this.multiplier + 1)]
            let TM = this.items[ci- (this.multiplier)]
            let TR = this.items[ci- (this.multiplier - 1)]
            let L = this.items[ci-1]
            let R = this.items[ci+1]
            let BL = this.items[ci+ (this.multiplier - 1)]
            let BM = this.items[ci+ (this.multiplier)]
            let BR = this.items[ci+ (this.multiplier + 1)]
            const places = [TL,TM,TR,L,R,BL,BM,BR]
            const leftPlaces = [TM,TR,R,BM,BR]
            const rightPlaces = [TL,TM,L,BL,BM]
            let score = 0
          if(ci % this.multiplier === 0){
            leftPlaces.forEach(x => {
              if(x !== undefined){
                score = score + x.id
                this.items[ci].score = score
                console.log('left!'+ ci)
              }
            })
          }
          else if((ci+1) % this.multiplier  === 0 ){
            rightPlaces.forEach(x => {
              if(x !== undefined){
                score = score + x.id
                this.items[ci].score = score
                console.log('right!'+ ci)
              }
            })
          }
          else{
            places.forEach(x => {
              if(x !== undefined){
                score = score + x.id
                this.items[ci].score = score
                console.log('normal!'+ ci)
              }
            })
          }
        },
        getAmount: function (){
        this.amount = this.PropAmount * 10
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
              score: number;
            }
          for(let i = 0; i < this.amount - (100 / this.amount) * this.difficulty; i++){
            let oob: T = {id: 0, name: 'neutral', score: 0}
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
