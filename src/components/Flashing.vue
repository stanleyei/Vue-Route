<template>
  <div class="flashing" :style="hasColor ? `background-color: ${color}` : ''">
    <input type="color" class="color" v-model="color">
  </div>
</template>

<script>
export default {
  name: "Flashing",
  data() {
    return {
      hasColor: true,
      color: '#ff0000',
    }
  },
  methods: {

  },
  mounted() {
    this.timer = setInterval(() => {
      this.hasColor = !this.hasColor;
    }, 500);
  },
  beforeUnmount() {
    if (this.timer) {
      window.clearInterval(this.timer); 
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  .flashing {
    width: 100%;
    height: 100%;

    .color {
      position: absolute;
      bottom: 0;
      right: 0;
    }
  }

</style>
