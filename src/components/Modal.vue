<template>
  <teleport to="body" v-if="!closeModel">
    <div class="modal fade" :id="`functionModal-${index}`" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">請選擇需要的功能</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true" class="text-white">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <div class="function-select mb-3" data-dismiss="modal" @click="sendToParent(1)">顯示時間</div>
              <div class="function-select mb-3" data-dismiss="modal" @click="sendToParent(2)">閃爍功能</div>
              <div class="function-select mb-3" data-dismiss="modal" @click="sendToParent(3)">系統狀態</div>
              <label class="function-select w-100">
                <span>放入圖片</span>
                <input type="file" accept=".jpg, .png" class="img-input" @change="previewFiles" :data-key="index">
              </label>
            </div>
          </div>
        </div>
    </div>
  </teleport>
</template>

<script>
export default {
  name: "Modal",
  props: {
    index: Number,
    close: Boolean,
  },
  data() {
    return {
      path: '',
      closeModel: this.close,
    }
  },
  methods: {
    sendToParent(type) {
      this.$parent.functionSelect[this.index].type = type
    },
    previewFiles(e) {
      const file = e.target.files[0];
      const reader = new FileReader();
      reader.onload = e => this.path = e.target.result;
      reader.readAsDataURL(file);

      this.sendToParent(4);
      this.closeModel = true;
      const modalBackdrop = document.querySelector('.modal-backdrop');
      const body = document.querySelector('body');
      body.removeChild(modalBackdrop);
      setTimeout(() => this.closeModel = false, 100);
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.modal-content {
    background-color: #2c3e50;
    font-weight: bold;

    .modal-title {
        color: #ffffff;
    }

    .function-select {
        padding: 10px 0;
        cursor: pointer;
        background-color: rgb(112, 211, 125);
        font-size: 20px;
        border-radius: 4px;
        text-align: center;

        &:hover {
            background-color: rgb(179, 226, 185);
        }

        .img-input {
            width: 0;
            height: 0;
        }
    }
}

</style>
