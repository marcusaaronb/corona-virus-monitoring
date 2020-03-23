<template>
  <v-toolbar class="indigo lighten-1 white--text">
    <v-toolbar-title>Corona Virus Monitoring</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat dark to="/">Home</v-btn>
      <v-btn flat dark to="/gallery">Gallery</v-btn>
    </v-toolbar-items>
    <v-btn flat icon dark @click="openGithub">
      <v-icon>public</v-icon>
    </v-btn>
  </v-toolbar>
</template>

<script>
export default {
  methods: {
    openGithub() {
      window.open(
        "https://github.com/marcusaaronb/corona-virus-monitoring",
        "_blank"
      );
    }
  }
};
</script>