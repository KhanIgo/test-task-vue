<template>
  <div class="TopBlock">
    <TopItem v-for="thing in things" :title="thing.name"  />
  </div>
</template>

<script>
import TopItem from "@/components/TopItem";

export default {
  name: "TopBlock",
  components: {TopItem},
  props: {
    things: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.TopBlock{
  display: flex;
  flex-wrap: wrap;
}
</style>
