<template>
  <div class="TopItem">
    <p>{{title}}</p>
  </div>
</template>

<script>
export default {
  name: "TopItem",
  props: {
    title: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
.TopItem{
  padding: 5px;
  margin: 5px;
  border: solid 1px dimgrey;
}

</style>
