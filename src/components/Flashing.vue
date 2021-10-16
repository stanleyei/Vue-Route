<template>
  <div class="flashing" :class="{red: hasColor}">
    <input type="color" class="color" v-model="color" @input="changeColor">
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
    changeColor(e) {
      e.target.parentElement.style.setProperty('--color', this.color);
    }
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

  $color: var(--color);

  .red {
    @if $color == true {
      background-color: var(--color);
    } @else {
      background-color: red;
    }
  }

</style>
