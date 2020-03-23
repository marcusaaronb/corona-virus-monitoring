<template>
  <div>
    <!-- Developer Information -->
    <v-container>
      <v-divider></v-divider>
      <h3>Developed By:</h3>
      <p>Marcus Aaron M. Baga</p>
    </v-container>

    <v-footer dark height="auto">
      <v-card flat tile class="indigo lighten-1 white--text text-xs-center">
        <v-card-text>
          <!-- <v-btn v-for="icon in icons" :key="icon" class="mx-3 white--text" icon>
            <v-icon size="24px">{{ icon }}</v-icon>
          </v-btn>-->
        </v-card-text>

        <v-card-text class="white--text pt-0">
          Coronavirus disease (COVID-19) is an infectious disease caused by a newly discovered coronavirus.
          Most people infected with the COVID-19 virus will experience mild to moderate respiratory illness and recover without requiring special treatment. Older people, and those with underlying medical problems like cardiovascular disease, diabetes, chronic respiratory disease, and cancer are more likely to develop serious illness.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-text class="white--text">&copy;{{ new Date().getFullYear() }}</v-card-text>
      </v-card>
    </v-footer>
  </div>
</template>

<script>
export default {};
</script>