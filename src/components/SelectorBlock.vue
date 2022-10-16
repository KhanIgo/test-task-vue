<template>

  <div class="SelectorBlock">
    <ul>
      <li v-for="thing in things">
        <Item :title="thing.name" :id="thing.id" :clickEventName="addEventName" :isSelected=isSelected(thing.id) />
      </li>
    </ul>

  </div>

</template>

<script>

import Item from "@/components/Item";
export default {
  name: "SelectorBlock",
  components: { Item },
  props: {
    things: {
      type: Array,
      required: true
    },
    selectedThings: {
      type: Array,
      required: true
    },
    addEventName: {
      type: String,
      required: false
    }
  },

  methods:{
    isSelected(id){
      let status = this.selectedThings.includes(id);
      return status;
    }
  }
}
</script>

<style scoped>

ul{
  list-style: none;
  display: flex;
  flex-wrap: wrap;
}
li{
  margin: 5px;
}
button{
  border: solid 1px dimgrey;
  padding: 5px;
  border-radius: 3px;
  background: transparent;

}
</style>
