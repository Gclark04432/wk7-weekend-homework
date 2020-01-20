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
  props: ['selectedItem', 'attachedItems'],
  methods: {
    validateAttachment: function () {
      const titleCheck = this.attachedItems.filter(item => item.type == "Title")

      if (this.selectedItem.type != "Title" || titleCheck.length == 0) {
        eventBus.$emit('attach-item', this.selectedItem)
        console.log("Test is working")
      }
    },
    attachItem: function () {
      this.validateAttachment()
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
