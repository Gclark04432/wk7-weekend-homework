<template>
  <div class="">
  <item-list :items="items"></item-list>
  <item-detail :selectedItem="selectedItem"></item-detail>
</div>
</template>

<script>
import { eventBus } from './main.js';
import ItemList from './components/ItemList.vue';
import ItemDetail from './components/ItemDetail.vue';

export default {
  name: 'app',
  data: function () {
    return {
      items: [],
      selectedItem: {}
    }
  },
  components: {
    'item-list': ItemList,
    'item-detail': ItemDetail
  },
  mounted: function () {
    fetch('https://xivapi.com/item')
    .then(results => results.json())
    .then(data => data.Results)
    .then(itemsFromApi => this.items = itemsFromApi.filter(item => !item.Name == ""))

    eventBus.$on('item-selected', selectedItem => this.selectedItem = selectedItem)

  }
}
</script>

<style lang="css" scoped>
</style>
