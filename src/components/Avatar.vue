<template lang="html">
  <section>
  </section>

</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'avatar',
  data: function () {
    return {
      title: null
    }
  }
}
</script>

<style lang="css" scoped>
section {
  background-image: url('../../public/avatar.png');
  background-repeat: no-repeat;
  height: 300px;
  width: 200px;
  background-size: contain;
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
}
</style>
