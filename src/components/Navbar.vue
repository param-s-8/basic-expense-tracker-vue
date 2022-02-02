<template>
  <v-app-bar app dark>
      <div class="d-flex align-center">
        <v-img
          alt="Track-It Logo"
          class="shrink mr-2"
          contain
          src="../assets/expense tracker.png"
          transition="scale-transition"
          width="40"
        />
        <v-toolbar-title class="text-h3">Track It</v-toolbar-title>
      </div>
      <v-spacer></v-spacer>
    </v-app-bar>
</template>

<script>

  export default {
      name: "Navbar"
  }

</script>

<style> </style>