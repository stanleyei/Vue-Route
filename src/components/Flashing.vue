<template>
  <div class="flashing" :class="{red: hasColor}">
    <input type="color" class="color" value="#ff00ff">
  </div>
</template>

<script>
export default {
  name: "Flashing",
  data() {
    return {
      hasColor: true,
    };
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

  .red {
    background: radial-gradient(circle at center,red,rgb(133, 55, 55));
  }
</style>
