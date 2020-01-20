<template lang="html">
  <div>
    <h2 v-if="titleExists()">{{ this.title.Name }}</h2>
    <section>
    </section>
  </div>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'avatar',
  data: function () {
    return {
      title: false
    }
  },
  methods: {
    titleExists: function () {
      const titleCheck = this.attachedItems.filter(item => item.type == "Title")
      this.title = titleCheck[0]
      return titleCheck.length == 1
    }
  },
  props:['attached-items']
}
</script>

<style lang="css" scoped>
section {
  background-image: url('../../public/avatar.png');
  background-repeat: no-repeat;
  height: 400px;
  width: 300px;
  background-size: contain;
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
}

h2 {
  color: darkred;
  font-family: fantasy;
  grid-row-start: 1;
  grid-row-end: 2;
}

</style>
