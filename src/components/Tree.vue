<template>
  <v-card class="mx-auto" max-width="500">
    <v-list>
      <v-list-item-content class="pl-5">
        <v-list-item-title class="title">My tree </v-list-item-title>
        <v-list-item-subtitle class="purple--text">
          Double click in a node to make it a folder
        </v-list-item-subtitle>
      </v-list-item-content>
      <Node
        @add-folder="makeFolder"
        @add-item="addItem"
        :item="treeData"
        class="item"
      ></Node>
    </v-list>
  </v-card>
</template>

<script>
import Vue from 'vue';

export default {
  name: 'Tree',
  components: {
    Node: () => import('./Node'),
  },

  data() {
    return {
      treeData: {
        name: 'Root',
        children: [
          {
            name: 'Parent Node',
            children: [
              {
                name: 'Parent Node',
                children: [{ name: 'Child Node' }, { name: 'Child Node' }],
              },
              { name: 'Sibling Node' },
              { name: 'Sibling Node' },
            ],
          },
          { name: 'Parent Node' },
          { name: 'Parent Node' },
        ],
      },
    };
  },
  methods: {
    makeFolder(item) {
      item.name = 'Parent Node';
      Vue.set(item, 'children', []);
      this.addItem(item);
    },
    addItem(item) {
      item.children.push({
        name: 'Child Node',
      });
    },
  },
};
</script>
