<template lang="html">
  <div>
    <h2>Attached {{ attachedTypeToDisplay }}(s): </h2>
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
    display: flex;
    align-items: center;
  }

  li {
    list-style: none;
    display: inline-flex;
  }

</style>
