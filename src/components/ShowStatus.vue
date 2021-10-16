<template>
  <div class="status-block">
    <div class="items" v-for="(state, key) in statusData" :key="key">
      <span>{{ state.name }}</span>
      <div class="status-color stable" v-if="state.value"></div>
      <div class="status-color unstable" v-else></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ShowStatus",
  data() {
    return {
      statusData: [],
    };
  },
  methods: {
    async getData() {
      try {
        const url = "https://www.dannyball710.net/api/list/";
        const res = await fetch(url);
        this.statusData = await res.json();
      } catch (err) {
        console.error(err);
      }
    },
  },
  mounted() {
    this.getData();
  },
  beforeUnmount() {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.status-block {
  width: 100%;
  height: 100%;
  font-size: 25px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .items {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    column-gap: 20px;

    .status-color {
      width: 60px;
      height: 30px;
      border: 2px solid black;
    }

    .stable {
      background-color: rgb(0, 255, 98);
    }

    .unstable {
      background-color: red;
    }
  }
}
</style>
