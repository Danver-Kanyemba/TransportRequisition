<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-btn to="/">home</v-btn>
      <v-btn to="/about">About</v-btn>
      <v-btn to="/login">Login</v-btn>
      <v-btn to="/Register">Register</v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
