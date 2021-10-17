<template>
  <h1>{{ time }}</h1>
</template>

<script>
export default {
  name: "ShowTime",
  data() {
    return {
      time: new Date().toLocaleTimeString('en-GB'),
    };
  },
  methods: {
    resetTime() {
      this.time = new Date().toLocaleTimeString('en-GB');
    },
  },
  created() {
    this.timer = setInterval(this.resetTime, 1000);
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
