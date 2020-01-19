<template lang="html">
  <div>
    <h2>Attached Items: </h2>
    <ul>
      <li v-for="item in attachedItems">{{item.Name}} <icon v-on:click="removeItem(item)">❌</icon></li>
    </ul>

  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'attached-items',
  props: ['attachedItems'],
  methods: {
    removeItem: function (item) {
      eventBus.$emit('remove-item', item)
    }
  }
}
</script>

<style lang="css" scoped>
span {
  z-index: 1;
}
</style>
