<template>
  <body>
    <div class="">
      <item-level-select :selectedLevel="selectedLevel"></item-level-select>
      <item-list :items="items"></item-list>
      <item-detail v-if="item-selected != null" :selectedItem="selectedItem"></item-detail>
    </div>
  </body>
</template>

<script>
import { eventBus } from './main.js';
import ItemList from './components/ItemList.vue';
import ItemDetail from './components/ItemDetail.vue';
import ItemLevelSelect from './components/ItemLevelSelect.vue';
import AttachedItems from './components/AttachedItems.vue';

export default {
  name: 'app',
  data: function () {
    return {
      selectedLevel: null,
      selectedType: null,
      items: [],
      selectedItem: null,
      attachedItems: null
    }
  },
  components: {
    'item-list': ItemList,
    'item-detail': ItemDetail,
    'item-level-select': ItemLevelSelect,
    'attached-items': AttachedItems
  },
  mounted: function () {

    eventBus.$on('item-selected', selectedItem => this.selectedItem = selectedItem)
    eventBus.$on('level-selected', selectedLevel => this.selectedLevel = selectedLevel)
    eventBus.$on('type-selected', selectedType => this.selectedType = selectedType)

  },
  watch: {
    selectedLevel: function () {
      fetch(`https://xivapi.com/search?filters=LevelItem=${this.selectedLevel}`)
        .then(results => results.json())
        .then(data => data.Results)
        .then(itemsFromApi => this.items = itemsFromApi.filter(item => !item.Name == ""))
      },
      selectedType: function () {
        fetch(`https://xivapi.com/${this.selectedType}`)
          .then(results => results.json())
          .then(data => data.Results)
          .then(itemsFromApi => this.items = itemsFromApi.filter(item => !item.Name == ""))
        }
      }
    }
    </script>

    <style lang="css" scoped>
      body {
        background-image: url("../public/background.png");
        background-repeat: no-repeat;
        background-size: cover;
        height: 700px;
      }
    </style>
