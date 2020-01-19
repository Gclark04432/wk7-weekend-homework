<template lang="html">
  <ul>
  <li v-for="item in items" v-on:click="handleClick(item)"> {{item.Name}} </li>
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
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  list-style: none;
}

</style>
