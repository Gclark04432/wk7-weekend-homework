<template lang="html">
  <div>
    <h1>{{selectedItem.Name}}</h1>
    <img :src="'https://xivapi.com/' + selectedItem.Icon" alt="NO ICON AVAILABLE">
    <br>
    <button type="button" v-on:click="attachItem" value="selectedItem">Attach Item</button>
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

  div {
    display: block;
    justify-content: center;
    align-content: center;
  }

</style>
