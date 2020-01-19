<template lang="html">
  <div>
    <h2 class="name">{{selectedItem.Name}}</h2>
    <img :src="'https://xivapi.com/' + selectedItem.Icon" alt="NO ICON AVAILABLE">
    <br>
    <button type="button" v-on:click="attachItem" value="selectedItem">Attach {{selectedItem.type}}</button>
  </div>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-detail',
  props: ['selectedItem'],
  methods: {
    attachItem: function () {
      // validateAttachment(this.selectedItem)
      eventBus.$emit('attach-item', this.selectedItem)
    },
    validateAttachment: function () {
      if (this.selectedItem.type == "title")
      console.log("Test is working");
    }
  }
}

</script>

<style lang="css" scoped>

div {
  display: grid;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  font-family: fantasy, sans-serif;
}

button {
  background-color: darkgoldenrod;
  color: white;
  text-emphasis: bold;
  font-size: 15px;
}

.name {
  text-transform: capitalize;
}

img {
  height: 150px;
  width: 150px;
}

</style>
