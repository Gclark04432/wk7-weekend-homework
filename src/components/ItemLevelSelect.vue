<template lang="html">
  <section>
    <form v-on:submit.prevent>

      <label for="levelSelect">Please select desired item level: </label>
      <select name="levelSelect" v-model="selectedLevel">
        <option disabled value selected></option>
        <option  v-for="level in itemLevelRange" :value="level">{{ level }}</option>
      </select>

      <label for="typeSelect">Please select the type of item: </label>
      <select name="typeSelect" v-model="selectedType">
        <option disabled value selected></option>
        <option value="Achievement">Achievement</option>
        <option value="Action">Action</option>
        <option value="Companion">Companion</option>
        <option value="Emote">Emote</option>
        <option value="Item">Item</option>
        <option value="Leve">Leve</option>
        <option value="Mount">Mount</option>
        <option value="Recipe">Recipe</option>
        <option value="Status">Status</option>
        <option value="Title">Title</option>
        <option value="Trait">Trait</option>
      </select>


    </form>
  </section>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-level-select',
  data: function () {
    return {
      itemLevelRange: [...Array(100).keys()],
      selectedLevel: null,
      selectedType: null
    }
  },
  watch: {
    selectedLevel: function() {
      eventBus.$emit('level-selected', this.selectedLevel)
    },
    selectedType: function () {
      eventBus.$emit('type-selected', this.selectedType)
    }
  }
}
</script>

<style lang="css" scoped>
  form {
    display: flex;
    justify-content: space-between;
  }
</style>
