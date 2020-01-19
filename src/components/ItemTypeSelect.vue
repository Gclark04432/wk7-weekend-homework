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

    </form>
  </section>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'item-type-select',
  data: function () {
    return {
      selectedType: null
    }
  },
  props: ['itemTypes'],
  watch: {
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
