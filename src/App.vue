<template>
  <v-app>
    <v-main>
      <Tree />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  components: {
    Tree: () => import('./components/Tree'),
  },
};
</script>
