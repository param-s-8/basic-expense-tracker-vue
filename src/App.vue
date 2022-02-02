<template>
  <v-app>
    <!-- <v-app-bar
      app
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Track-It Logo"
          class="shrink mr-2"
          contain
          src="./assets/expense tracker.png"
          transition="scale-transition"
          width="40"
        />

        <v-toolbar-title>Track It</v-toolbar-title>
      </div>

      <v-spacer></v-spacer>

      
    </v-app-bar> -->

    <Navbar/>
    <v-main>
      <Dashboard/>
      <v-container
    id="input-usage"
    fluid
  >
  </v-container>

    </v-main>
  </v-app>
</template>

<script>
import Dashboard from './components/Dashboard';
import Navbar from './components/Navbar.vue';


export default {
  name: 'App',

  components: {
    Dashboard,
    Navbar
  },

  data: () => ({
    //
  }),
};
</script>
