<template>
  <h1>{{ time }}</h1>
</template>

<script>
export default {
  name: "ShowTime",
  data() {
    return {
      time: new Date(),
    };
  },
  methods: {
    computedTime() {
      const now = new Date();
      this.time = now.toLocaleTimeString();
    },
  },
  mounted() {
    this.computedTime();
    const vm = this;
    this.timer = setInterval(() => {
      const now = new Date();
      vm.time = now.toLocaleTimeString();
    }, 1000);
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

  h1 {
    font-size: 60px;
  }

</style>
