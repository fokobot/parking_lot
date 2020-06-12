<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-btn to="/" text>
          <v-icon large>local_parking</v-icon>
          <span class="mr-2">Parking Lot</span>
        </v-btn>
      </div>

      <v-spacer></v-spacer>

      <v-btn to="/about" text>
        <span class="mr-2">About</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    //
  }),
};
</script>
