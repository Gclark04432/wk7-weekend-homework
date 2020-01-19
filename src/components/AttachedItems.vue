<template lang="html">
  <div>
    <h2>Attached Items: </h2>
    <ul>
      <li v-for="item in attachedItems">{{item.Name}}</li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'attached-items',
  props: ['attachedItems']
}
</script>

<style lang="css" scoped>
</style>
