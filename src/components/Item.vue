<template>

  <button @click="clickHandler">
    {{title}}
  </button>

</template>

<script>
export default {
  name: "Item",
  props: {
    title: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    },
    isSelected: {
      type: Boolean,
      required: false
    },
    clickEventName: {
      type: String,
      required: false
    }
  },
  methods: {
    clickHandler(){
      this.$root.$emit(this.clickEventName, this.id);
    }
  }
}
</script>

<style scoped>

</style>
