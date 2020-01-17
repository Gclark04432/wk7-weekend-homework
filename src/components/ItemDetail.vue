<template lang="html">
  <div>
    <h1>{{selectedItem.Name}}</h1>
    <h3>{{selectedItem.Icon}}</h3>
  </div>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-detail',
  data: function () {
    return {
    }
  },
  props: ['selectedItem'],
  mounted: function () {
  }
}
</script>

<style lang="css" scoped>
</style>
