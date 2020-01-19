<template lang="html">
  <div>
    <h1>Attached {{ attachedTypeToDisplay }}(s)</h1>
    <ul>
      <li v-for="item in this.type">{{item.Name}} <icon v-on:click="removeItem(item)">❌</icon></li>
    </ul>

  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'attached-items',
  props: ['attachedItems', 'attachedTypeToDisplay'],
  methods: {
    removeItem: function (item) {
      eventBus.$emit('remove-item', item)
    }
  },
  computed: {
    type: function () {
      return this.attachedItems.filter(item => item.type == this.attachedTypeToDisplay)
    }
  }
}
</script>

<style lang="css" scoped>

  div {
    display: grid;
    grid-template-columns: 1fr;
    justify-content: center;
  }

  li {
    list-style: none;
  }

</style>
