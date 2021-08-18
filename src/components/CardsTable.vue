<template>
  <div>
    <card v-for="card in $store.state.table" :key="card.id" :id="card.id" />
  </div>
</template>

<script>
import Card from './Card.vue'

export default {
  components: {
    Card
  }
}
</script>

<style scoped lang="scss">
  @import "./styles/cardstable.scss";
</style>
