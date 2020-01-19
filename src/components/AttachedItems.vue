<template lang="html">
  <div>
    <h2>Attached {{ attachedTypeToDisplay }}(s): </h2>
    <ul>
      <li class="name" v-for="item in this.type">{{item.Name}} <span v-on:click="removeItem(item)">❌</span></li>
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
    font-family: fantasy, sans-serif;
  }

  li {
    list-style: none;
    display: inline-flex;
  }

  .name {
    text-transform: capitalize;
  }

</style>
