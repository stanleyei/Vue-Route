<template>
  <img :src="path" alt="" class="w-100">
</template>

<script>
export default {
  name: 'ShowPicture',
  props: {
    path:String,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  img {
    height: 100%;
  }
</style>
