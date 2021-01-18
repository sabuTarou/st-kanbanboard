<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">KANBAN BOARD</div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main class="mt-4 mr-4 ml-4">
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  // components: {
  //   HelloWorld,
  // },

  data: () => ({
    //
  }),
};
</script>

<style lang="scss">
html {
  height: 100%;
}
body {
  height: 100%;
  margin: 0;
}
#app {
  height: 100%;
  margin: 0;
  background-color: #e9ecef;
}
</style>
