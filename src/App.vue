<template>
  <div id="app" class="app">
    <div class="app-row">
      <div v-if="getLeftThings.length" class="app-item  "><TopBlock :things="getLeftThings" /></div>
      <div v-if="getRightThings.length" class="app-item app-item_right"><TopBlock :things="getRightThings" /></div>
    </div>

    <div class="app-row">
      <div class="app-item"><SelectorBlock :things="leftThings" :selectedThings="leftThingsSelected" :addEventName="'AddItemToLeft'" /></div>
      <div class="app-item"><SelectorBlock :things="rightThings" :selectedThings="rightThingsSelected" :addEventName="'AddItemToRight'"  /></div>
    </div>
  </div>
</template>

<script>

import SelectorBlock from "@/components/SelectorBlock";
import TopBlock from "@/components/TopBlock";
import {uniq} from "lodash";
export default {
  name: 'App',
  components: {
    TopBlock,
    SelectorBlock
  },

  data() {
    return {

      leftThings: [
        {
          id: 1,
          name: "Shoes 1"
        },
        {
          id: 2,
          name: "Shoes 2"
        },
        {
          id: 3,
          name: "Shoes 3"
        },
        {
          id: 4,
          name: "Shoes 4"
        },
        {
          id: 5,
          name: "T-shirt 1"
        },
        {
          id: 6,
          name: "T-shirt 2"
        },
        {
          id: 7,
          name: "T-shirt 3"
        },
        {
          id: 8,
          name: "T-shirt 4"
        }
      ],
      rightThings: [
        {
          id: 11,
          name: "Jacket 1"
        },
        {
          id: 12,
          name: "Jacket 2"
        },
        {
          id: 13,
          name: "Jacket 3"
        },
        {
          id: 14,
          name: "Jacket 4"
        },
        {
          id: 15,
          name: "Hoodie 1"
        },
        {
          id: 16,
          name: "Hoodie 2"
        },
        {
          id: 17,
          name: "Hoodie 3"
        },
        {
          id: 18,
          name: "Hoodie 4"
        }
      ],
      leftThingsMaxSelect: 6,
      rightThingsMaxSelect: 1,
      leftThingsSelected: [],
      rightThingsSelected: [],
    }
  },
  computed: {
    getLeftThings(){
      return this.getItemsForTopBlock(this.leftThings, this.leftThingsSelected)
    },
    getRightThings(){
      return this.getItemsForTopBlock(this.rightThings, this.rightThingsSelected)
    }
  },
  methods:{
    addItem(id, type){
      if (type=='left'){
        this.leftThingsSelected.unshift(id);
        this.leftThingsSelected=uniq(this.leftThingsSelected)
        this.leftThingsSelected= this.leftThingsSelected.splice(0, this.leftThingsMaxSelect)
      }
      else if (type=='right'){
        this.rightThingsSelected.unshift(id);
        this.rightThingsSelected=uniq(this.rightThingsSelected)
        this.rightThingsSelected= this.rightThingsSelected.splice(0, this.rightThingsMaxSelect)
      }
    },
    getItemsForTopBlock(allItems, selectedItems){
      let res = [];
      res = allItems.filter(item=>{
        return selectedItems.includes(item.id);
      });
      res.sort((a,b)=>{
        return selectedItems.indexOf(a.id)-selectedItems.indexOf(b.id)
      })
      return res;
    }
  },
  mounted() {
    this.$root.$on('AddItemToLeft', id=>{
      this.addItem(id, 'left');
    });
    this.$root.$on('AddItemToRight', id=>{
      this.addItem(id, 'right');
    });
  }
}
</script>

<style lang="scss">
*{
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.app{
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
}
.app-row{
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.app-item{
  width: 47%;
  flex-shrink: 0;
  flex-grow: 0;
  margin: 10px 0;
  border: solid 1px gray;
  border-radius: 3px;
  padding: 5px;

  &_right{
    margin-left: auto;
  }
}
</style>
