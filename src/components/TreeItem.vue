<template>
  <li>
    <div :class="[{bold: isFolder}, 'pointer']" @click="toggle(item.id)">
      {{ item.name }}
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
    </div>
    <ul v-show="isOpen" v-if="isFolder">
      <tree-item
          class="item"
          v-for="(child, index) in item.children"
          :key="index"
          :item="child"
      ></tree-item>
    </ul>
  </li>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: false,
      default: () => {}
    }
  },
  data: () => ({
    isOpen: false,
  }),
  computed: {
    isFolder () {
      return this.item.children && this.item.children.length;
    },
  },
  methods: {
    toggle(id) {
      this.isOpen = !this.isOpen
      localStorage.setItem('selectId', id)
    }
  }
}
</script>

<style>
.bold {
  font-weight: bold;
}
.pointer {
  cursor: pointer;
}
</style>