<template>
  <v-card class="mx-auto" max-width="500">
    <v-list>
      <v-subheader>My Tree</v-subheader>
      <Node
        class="item"
        :item="treeData"
        @add-folder="makeFolder"
        @add-item="addItem"
      ></Node>
    </v-list>
  </v-card>
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
          { name: "Parent Node" },
          { name: "Parent Node" },
          {
            name: "Parent Node",
            children: [
              {
                name: "Sibling Node",
                children: [{ name: "Child Node" }, { name: "Child Node" }],
              },
              { name: "Sibling Node" },
              { name: "Sibling Node" },
            ],
          },
        ],
      },
    };
  },
  methods: {
    makeFolder(item) {
      item.name = "Parent Node";
      Vue.set(item, "children", []);
      this.addItem(item);
    },
    addItem(item) {
      item.children.push({
        name: "Child Node",
      });
    },
  },
};
</script>
