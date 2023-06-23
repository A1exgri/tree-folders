<template>
  <div :class="[{show: isShowModal} ,'modal fade']">
    <div class="modal-shadow" />
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">{{ title }}</h5>
        </div>
        <div class="modal-body">
          <ul>
            <tree-item
                v-for="item in folders"
                :key="item.id"
                class="item"
                :item="item"
            ></tree-item>
          </ul>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn" @click="closeModal">Ок</button>
          <button type="button" class="btn btn-outline" @click="closeModal">Закрыть</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TreeItem from "@/components/TreeItem";

export default {
  components: {
    TreeItem
  },
  props: {
    title: {
      type: String,
      required: true
    },
    isShowModal: {
      type: Boolean,
      required: false,
      default: false
    },
    folders: {
      type: Array,
      required: false,
      default: () => []
    }
  },
  methods: {
    closeModal() {
      this.$emit('select', {
        isShowModal: false,
        selectId: this.selectId
      })
    }
  }
}
</script>

<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  display: none;
  width: 100%;
  height: 100%;
  overflow: hidden;
  outline: 0;
  background: rgba(0,0,0,.5);
}
.modal.show {
  display: block;
}
.fade {
  transition: opacity .15s linear;
}
.modal-dialog {
  max-width: 500px;
  margin: 1.75rem auto;
}
.modal-content {
  position: relative;
  display: flex;
  flex-direction: column;
  width: 100%;
  pointer-events: auto;
  background-color: #fff;
  border: 1px solid rgba(0,0,0,.2);
  border-radius: 0.3rem;
  outline: 0;
}
.modal-header {
  display: -ms-flexbox;
  display: flex;
  -ms-flex-align: start;
  align-items: flex-start;
  -ms-flex-pack: justify;
  justify-content: space-between;
  padding: 1rem 1rem;
  border-bottom: 1px solid #dee2e6;
  border-top-left-radius: calc(0.3rem - 1px);
  border-top-right-radius: calc(0.3rem - 1px);
}
.modal-title {
  margin: 0;
  line-height: 1.5;
  font-size: 20px;
}
.modal-body {
  position: relative;
  flex: 1 1 auto;
  padding: 1rem;
}
.modal-footer {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: flex-end;
  padding: 0.75rem;
  border-top: 1px solid #dee2e6;
  border-bottom-right-radius: calc(0.3rem - 1px);
  border-bottom-left-radius: calc(0.3rem - 1px);
}
.modal-footer .btn{
  margin-right: 10px;
}
</style>
