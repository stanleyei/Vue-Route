<template>
  <main>
    <div class="home mb-5">
      <img alt="Vue logo" src="@/assets/logo.png">
    </div>
    <div class="container">
      <div class="function-block" :class="{pointer: !functionExist(key), grab: functionExist(key)}" data-toggle="modal" :data-target="functionExist(key) ? '#' : `#functionModal-${key}`" v-for="(select, key) in functionSelect" :key="select.id" draggable="true" @dragstart="startDrag($event, key, select.type)" @dragend="endDrag" @drop="onDrop($event, key, select.type)" @dragover.prevent>
        <button class="reset-btn rounded-circle text-white" title="取消" @click="reset(key)" v-if="functionExist(key)">&times;</button>
        <component :is="functionSelect[key].name" :path="functionSelect[key].picturePath"/>
        <span v-if="functionSelect[key].type === 0">+</span>
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
        id: 0,
        type: 0,
        picturePath: '',
        name: ''
      },
      {
        id: 1,
        type: 0,
        picturePath: '',
        name: '',
      },
      {
        id: 2,
        type: 0,
        picturePath: '',
        name: '',
      },
      {
        id: 3,
        type: 0,
        picturePath: '',
        name: '',
      }],
    }
  },
  watch: {
    functionSelect: {
      deep: true,
      handler: function () {
        this.functionSelect.forEach(select => {
          if (select.type === 0) select.name = '';
          if (select.type === 1) select.name = 'ShowTime';
          if (select.type === 2) select.name = 'Flashing';
          if (select.type === 3) select.name = 'ShowStatus';
          if (select.type === 4) select.name = 'ShowPicture';
        });
      }
    }
  },
  methods: {
    reset(key) {
      this.functionSelect[key].type = 0;
    },
    functionExist(key) {
      if(this.functionSelect[key].type > 0) return true;
    },
    getWsData() {
      let ws = new WebSocket('ws://localhost:8100');
      ws.onopen = () => {
        console.log('open connection')
      }

      ws.onmessage = message => {
        console.log(message);
      }
    },
    startDrag(e, id, type) {
      e.dataTransfer.setData('type', type);
      e.dataTransfer.setData('itemID', id);
    },
    onDrop(e, endDragID, endDragType) {
      const startDragType = e.dataTransfer.getData('type');
      const startDragID = e.dataTransfer.getData('itemID');
      const startDragItem = this.functionSelect.find((select) => select.id === Number(startDragID));
      const endDragItem = this.functionSelect.find((select) => select.id === endDragID);
      endDragItem.type = Number(startDragType);
      startDragItem.type = endDragType;
    },
    endDrag (e) {
      e.dataTransfer.clearData();
    }
  },
  mounted() {
    // this.getWsData();
  },
  // beforeUnmount() {
  //   ws.onclose = () => {
  //     console.log('close connection')
  //   }
  // },
}
</script>

<style scoped lang="scss">

@import '@/assets/scss/main.scss';

</style>
