<template>
  <ul>
    <Node
      class="item"
      :item="treeData"
      @add-folder="makeFolder"
      @add-item="addItem"
    ></Node>
  </ul>
</template>

<script>
import Vue from "vue";

export default {
  name: "Tree",
  components: {
    Node: () => import("./Node"),
  },

  data() {
    return {
      treeData: {
        name: "Root",
        children: [
          { name: "Folder" },
          { name: "Folder" },
          {
            name: "Folder",
            children: [
              {
                name: "Folder",
                children: [{ name: "Folder" }, { name: "Folder" }],
              },
              { name: "Folder" },
              { name: "Folder" },
            ],
          },
        ],
      },
    };
  },
  methods: {
    makeFolder(item) {
      Vue.set(item, "children", []);
      this.addItem(item);
    },
    addItem(item) {
      item.children.push({
        name: "Folder",
      });
    },
  },
};
</script>
