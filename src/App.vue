<template>
  <div class="">
    <item-level-select :selectedLevel="selectedLevel"></item-level-select>
    <item-list :items="items"></item-list>
    <item-detail :selectedItem="selectedItem"></item-detail>
  </div>
</template>

<script>
import { eventBus } from './main.js';
import ItemList from './components/ItemList.vue';
import ItemDetail from './components/ItemDetail.vue';
import ItemLevelSelect from './components/ItemLevelSelect.vue';

export default {
  name: 'app',
  data: function () {
    return {
      selectedLevel: null,
      items: [],
      selectedItem: {}
    }
  },
  components: {
    'item-list': ItemList,
    'item-detail': ItemDetail,
    'item-level-select': ItemLevelSelect
  },
  mounted: function () {
    fetch(`https://xivapi.com/search?filters=LevelItem=${this.selectedLevel}`)
    .then(results => results.json())
    .then(data => data.Results)
    .then(itemsFromApi => this.items = itemsFromApi.filter(item => !item.Name == ""))

    eventBus.$on('item-selected', selectedItem => this.selectedItem = selectedItem)
    eventBus.$on('level-selected', selectedLevel => this.selectedLevel = selectedLevel)

  }
}
</script>

<style lang="css" scoped>
</style>
