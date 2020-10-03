<template>
  <li>
    <div @click="addFolder" @dblclick="toggle">
      {{ item.name }} {{ index }}
      <span v-if="isFolder">[{{ isOpen ? "-" : "+" }}]</span>
    </div>
    <ul v-show="isOpen" v-if="isFolder">
      <Node
        class="item"
        v-for="(child, index) in item.children"
        :key="index"
        :item="child"
        :index="index"
        @add-folder="$emit('add-folder', $event)"
        @add-item="$emit('add-item', $event)"
      ></Node>
      <li class="add" @click="$emit('add-item', item)">+</li>
    </ul>
  </li>
</template>

<script>
export default {
  name: "Node",
  props: {
    item: Object,
    index: Number,
  },
  data() {
    return {
      isOpen: true,
    };
  },
  computed: {
    isFolder() {
      return this.item.children && this.item.children.length;
    },
  },
  methods: {
    toggle() {
      if (this.isFolder) this.isOpen = !this.isOpen;
    },
    addFolder() {
      if (!this.isFolder) {
        this.$emit("add-folder", this.item);
        this.isOpen = true;
      }
    },
  },
};
</script>
