<template>
  <body>
    <header>
    </header>

    <div class="container">
      <item-level-select :selectedLevel="selectedLevel"></item-level-select>
      <item-list class="item-list" :items="items"></item-list>
      <item-detail class="item-detail" v-if="item-selected != null" :selectedItem="selectedItem"></item-detail>
      <attached-items class="attached-items" :attachedItems="attachedItems"></attached-items>
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
      attachedItems: []
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
    eventBus.$on('attach-item', selectedItem => this.attachedItems.push(selectedItem))

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
        height: 100%;
        width: 100%;
        position: fixed;
        padding: 5px;
      }

      header {
        background-image: url("../public/banner.png");
        height: 100px;
        background-repeat: no-repeat;
        background-size: contain;
        background-position: center center;
      }

      .container {
        display: grid;
        grid-gap: 15px;
        grid-template-columns: auto auto auto;
        grid-template-rows: 80px 200px;
      }

      .item-list {
        grid-column-start: 1;
        grid-column-end: 2;
        grid-row-start: 2;
        grid-row-end: 3;
      }

      .item-detail {
        grid-column-start: 2;
        grid-column-end: 3;
        grid-row-start: 2;
        grid-row-end: 3;
      }

      .attached-items {
        grid-column-start: 3;
        grid-column-end: 4;
        grid-row-start: 2;
        grid-row-end: 3;
      }

    </style>
