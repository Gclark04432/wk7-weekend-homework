<template>
  <body>
    <header>
    </header>

    <div class="container">
      <item-type-select class="select" :itemTypes="itemTypes"></item-type-select>
      <item-list class="item-list" :items="items"></item-list>
      <item-detail class="item-detail" v-if="selectedItem != ''" :selectedItem="selectedItem"></item-detail>
      <attached-items
      class="attached-items" :attachedItems="attachedItems" :attachedTypeToDisplay="attachedTypeToDisplay"
      v-if="!attachedItems.length == 0">
    </attached-items>
    <span>View Attchments by Type:
    <select class="attached-type" v-model="attachedTypeToDisplay">
      <option v-for="type in itemTypes" :value="type">{{ type }}</option>
    </select>
    </span>
    <avatar class="avatar"></avatar>
  </div>
</body>
</template>

<script>
import { eventBus } from './main.js';
import ItemList from './components/ItemList.vue';
import ItemDetail from './components/ItemDetail.vue';
import ItemTypeSelect from './components/ItemTypeSelect.vue';
import AttachedItems from './components/AttachedItems.vue';
import Avatar from './components/Avatar.vue';

export default {
  name: 'app',
  data: function () {
    return {
      selectedType: null,
      items: [],
      selectedItem: "",
      attachedItems: [],
      attachedTypeToDisplay: null,
      itemTypes: ['Achievement', 'Action', 'Companion', 'Emote', 'Item', 'Mount', 'Recipe', 'Status', 'Title', 'Trait']
    }
  },
  components: {
    'item-list': ItemList,
    'item-detail': ItemDetail,
    'item-type-select': ItemTypeSelect,
    'attached-items': AttachedItems,
    'avatar': Avatar
  },
  mounted: function () {

    eventBus.$on('item-selected', selectedItem => this.selectedItem = selectedItem)
    eventBus.$on('type-selected', selectedType => this.selectedType = selectedType)
    eventBus.$on('attach-item', selectedItem => {
      if (!this.attachedItems.includes(selectedItem)) {
        this.attachedItems.push(selectedItem)
      }
      else {
        alert("Already Attached")
      }
    })
    eventBus.$on('remove-item', item => this.attachedItems.pop(item))

  },
  methods: {
    appendType: function () {
      this.items.forEach(item => item.type = this.selectedType)
    }
  },
  watch: {
    selectedType: function () {
      fetch(`https://xivapi.com/${this.selectedType}`)
        .then(results => results.json())
        .then(data => data.Results)
        .then(itemsFromApi => {
          this.items = itemsFromApi.filter(item => !item.Name == "")
          this.appendType()
        })
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
    padding: 8px;
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
    grid-gap: 20px;
    grid-template-columns: 1fr 1fr 2fr 1fr;
    grid-template-rows: 20px 30px 200px;
    justify-content: space-evenly;
  }

  .item-list {
    grid-column-start: 1;
    grid-column-end: 2;
    grid-row-start: 3;
    grid-row-end: 4;
  }

  .item-detail {
    grid-column-start: 2;
    grid-column-end: 3;
    grid-row-start: 3;
    grid-row-end: 4;
  }

  .attached-items {
    grid-column-start: 2;
    grid-column-end: 4;
    grid-row-start: 1;
    grid-row-end: 2;
  }

  .attached-type {
    grid-column-start: 1;
    grid-column-end: 2;
    grid-row-start: 1;
    grid-row-end: 2;
  }

  .avatar {
    grid-column-start: 3;
    grid-column-end: 4;
    grid-row-start: 3;
    grid-row-end: 4;
  }

  .select {
    grid-column-start: 1;
    grid-column-end: 2;
    grid-row-start: 2;
    grid-row-end: 3;
    align-self: flex-end;
  }

  </style>
