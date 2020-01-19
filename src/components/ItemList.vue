<template lang="html">
  <ul>
    <li class="name" v-for="item in items" v-on:click="handleClick(item)"> {{item.Name}} </li>
  </ul>
</template>

<script>
import { eventBus} from '../main.js';

export default {
  name: 'item-list',
  data: function () {
    return {
      itemType: null
    }
  },
  props: ['items'],
  methods: {
    handleClick: function (item) {
      eventBus.$emit('item-selected', item)
    }
  }
}
</script>

<style lang="css" scoped>

ul {
  overflow: scroll;
  list-style: none;
  height: 400px;
  width: 250px;
  background: rgba(204, 204, 204, 0.5);
  border: 2px solid darkgoldenrod;
}

.name {
  text-transform: capitalize;
}

</style>
