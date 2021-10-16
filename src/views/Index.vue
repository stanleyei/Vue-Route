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
        <Modal :index="key" :close="closeModel"/>
      </div>
    </div>
  </main>
  <!-- <teleport to="body" v-if="!closeModel">
    <div class="modal fade" :id="`functionModal-${key}`" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" v-for="(model, key) in functionSelect" :key="key">
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">請選擇需要的功能</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true" class="text-white">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <div class="function-select mb-3" data-dismiss="modal" @click="functionSelect[key].type = 1">顯示時間</div>
              <div class="function-select mb-3" data-dismiss="modal" @click="functionSelect[key].type = 2">閃爍功能</div>
              <div class="function-select mb-3" data-dismiss="modal" @click="functionSelect[key].type = 3">系統狀態</div>
              <label class="function-select w-100">
                <span>放入圖片</span>
                <input type="file" accept=".jpg, .png" class="img-input" @change="previewFiles" :data-key="key">
              </label>
            </div>
          </div>
        </div>
    </div>
  </teleport> -->
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
      closeModel: false,
    }
  },
  methods: {
    reset(key) {
      this.functionSelect[key].type = 0;
    },
    functionExist(key) {
      if(this.functionSelect[key].type !== 0) return true;
    },
    previewFiles(e) {
      const file = e.target.files[0];
      const key = e.target.dataset.key;
      const reader = new FileReader();
      const select = this.functionSelect[key];
      reader.onload = e => select.picturePath = e.target.result;
      reader.readAsDataURL(file);

      select.type = 4;
      this.closeModel = true;
      const modalBackdrop = document.querySelector('.modal-backdrop');
      const body = document.querySelector('body');
      body.removeChild(modalBackdrop);
      setTimeout(() => this.closeModel = false, 100);
    },
  },
}
</script>

<style scoped lang="scss">

@import '@/assets/scss/main.scss';

</style>
