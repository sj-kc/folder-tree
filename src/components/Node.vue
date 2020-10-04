<template>
  <v-list-item-content>
    <v-list-item @click="toggle" @dblclick="addFolder">
      <v-icon v-if="isFolder">{{
        isOpen ? "mdi mdi-folder-open" : "mdi mdi-folder"
      }}</v-icon>

      <v-list-item-title class="pl-4">
        {{ item.name }} {{ index }}</v-list-item-title
      >
    </v-list-item>
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
      <v-list-item-content class="pl-9" @click="$emit('add-item', item)">
        +</v-list-item-content
      >
    </ul>
  </v-list-item-content>
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
