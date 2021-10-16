<template>
  <main>
    <div class="home mb-5">
      <img alt="Vue logo" src="@/assets/logo.png">
    </div>
    <div class="container">
      <div class="function-block" :class="{pointer: !functionExist(key)}" data-toggle="modal" :data-target="functionExist(key) ? '#' : `#functionModal-${key}`" v-for="(select, key) in functionSelect" :key="key" draggable="true">
        <button class="reset-btn rounded-circle text-white" title="取消" @click="reset(key)" v-if="functionExist(key)">&times;</button>
        <ShowTime v-if="functionSelect[key].type === 1"/>
        <Flashing v-else-if="functionSelect[key].type === 2"/>
        <ShowStatus v-else-if="functionSelect[key].type === 3"/>
        <ShowPicture :path="functionSelect[key].picturePath" v-else-if="functionSelect[key].type === 4"/>
        <span v-else>+</span>
        <Modal :index="key"/>
      </div>
    </div>
  </main>
</template>

<script>
import ShowPicture from '@/components/ShowPicture.vue'
import ShowTime from '@/components/ShowTime.vue'
import Flashing from '@/components/Flashing.vue'
import ShowStatus from '@/components/ShowStatus.vue'
import Modal from '@/components/Modal.vue'

export default {
  name: "Index",
  components: {
    ShowPicture,ShowTime,Flashing,ShowStatus,Modal
  },
  data() {
    return {
      functionSelect: [
      {
        type: 0,
        picturePath: '',
      },
      {
        type: 0,
        picturePath: '',
      },
      {
        type: 0,
        picturePath: '',
      },
      {
        type: 0,
        picturePath: '',
      }],
    }
  },
  methods: {
    reset(key) {
      this.functionSelect[key].type = 0;
    },
    functionExist(key) {
      if(this.functionSelect[key].type > 0) return true;
    },
  },
}
</script>

<style scoped lang="scss">

@import '@/assets/scss/main.scss';

</style>
