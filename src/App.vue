<template>
  <div class="container">
    <button class="btn" @click="isShowModal=!isShowModal">
      Открыть
    </button>
    <ModalComponent
        :is-show-modal="isShowModal"
        :title="title"
        :folders="foldersTree"
        @select="select"
    />
    <div v-if="selectId">
      <h4>
        Вы выбрали паппку с id: <em>{{selectId}}</em>
      </h4>
    </div>
  </div>
</template>

<script>
import ModalComponent from '@/components/ModalComponent'

export default {
  name: 'App',
  components: {
    ModalComponent
  },
  data: () => ({
    title: 'Дерево папок',
    isShowModal: false,
    foldersTree: [
      { id: 1, name: "Пустая папка" },
      { id: 2, name: "Пустая папка" },
      {
        id: 3,
        name: "Непустая папка",
        children: [
          {
            id:31,
            name: "Вложенная непустая папка",
            children: [
              { id: 311, name: "Папка"},
              {id: 312, name: "Папка"}
            ]
          },
          { id: 32, name: "Пустая папка" },
          { id: 33, name: "Пустая папка" },
          {
            id: 34,
            name: "Непустая папка",
            children: [
              { id: 341, name: "Пустая папка" },
              { id: 342, name: "Пустая папка" }
            ]
          }
        ]
      }
    ],
    selectId: null
  }),
  methods: {
    select(data) {
      this.isShowModal = data.isShowModal
      if(data.selectId) this.selectId = data.selectId
      else this.selectId = null
    }
  }
}
</script>

<style>
.container {
  width: 100%;
  max-width: 1140px;
  margin: 0 auto;
  padding: 15px 0;
}
.btn {
  color: #fff;
  background-color: #007bff;
  font-weight: 400;
  cursor: pointer;
  text-align: center;
  vertical-align: middle;
  user-select: none;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  border: 1px solid #007bff;
  transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}
.btn-outline {
  background-color: #fff;
  color: #007bff;
}
.btn:hover {
  color: #fff;
  background-color: #0069d9;
  border-color: #0062cc;
}

</style>
