<template lang="html">
  <section>
    <form v-on:submit.prevent>

      <div class="select">
        <label for="typeSelect">Please select the type of item: </label>
        <select name="typeSelect" v-model="selectedType">
          <option disabled value selected></option>
          <option v-for="type in itemTypes" :value="type">{{ type }}</option>
        </select>
      </div>

      <div class="select">
        <label for="levelSelect">Please select desired item level: </label>
        <select name="levelSelect" v-model="selectedLevel">
          <option disabled value selected></option>
          <option  v-for="level in itemLevelRange" :value="level">{{ level }}</option>
        </select>
      </div>


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
  props: ['itemTypes'],
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
  flex-direction: column;

}
</style>
