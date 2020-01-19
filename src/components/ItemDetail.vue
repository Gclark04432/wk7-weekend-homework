<template lang="html">
    <div>
      <h1>{{selectedItem.Name}}</h1>
      <img :src="'https://xivapi.com/' + selectedItem.Icon">
      <button type="button" name="attachItemButton">Show Me</button>
    </div>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-detail',
  props: ['selectedItem'],
}
</script>

<style lang="css" scoped>
</style>
