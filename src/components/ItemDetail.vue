<template lang="html">
  <div>
    <h1>{{selectedItem.Name}}</h1>
    <img :src="'https://xivapi.com/' + selectedItem.Icon" alt="NO ICON AVAILABLE">
    <button type="button" v-on:click="attachItem" value="selectedItem">Show Me</button>
  </div>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-detail',
  props: ['selectedItem'],
  methods: {
    attachItem: function () {
      eventBus.$emit('attach-item', this.selectedItem)
    }
  }
}

</script>

<style lang="css" scoped>
</style>
