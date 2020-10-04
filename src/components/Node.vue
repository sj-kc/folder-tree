<template>
  <v-list-item-content>
    <v-list-item @click="toggle" @dblclick="addFolder">
      <v-icon v-if="isFolder">
        {{ isOpen ? "mdi mdi-folder-open" : "mdi mdi-folder" }}
      </v-icon>

      <v-list-item-title class="pl-4">
        {{ item.name }} {{ index }}
      </v-list-item-title>
    </v-list-item>
    <ul v-show="isOpen" v-if="isFolder">
      <Node
        v-for="(child, index) in item.children"
        :key="index"
        :item="child"
        :index="index"
        @add-folder="$emit('add-folder', $event)"
        @add-item="$emit('add-item', $event)"
        title="Double click in a node to make it a folder"
        class="item"
      />
      <v-list-item-content
        @click="$emit('add-item', item)"
        title="Add node"
        class="pl-9"
      >
        +
      </v-list-item-content>
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
