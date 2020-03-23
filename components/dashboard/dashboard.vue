<template>
  <v-container grid-list-md>
    <v-content>
      <v-layout>
        <v-flex xs4 sm4 md4 v-for="all in all" :key="all.name">
          <v-card :color="all.color" dark>
            <v-card-title primary-title>
              <div>
                <div class="headline">{{ all.name }}</div>
                <div class="align-end">{{ all.count }}</div>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
      </v-layout>
    </v-content>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    all: [
      {
        name: "Cases",
        count: 0,
        color: "blue"
      },
      {
        name: "Deaths",
        count: 0,
        color: "red"
      },
      {
        name: "Recovered",
        count: 0,
        color: "green"
      }
    ]
  }),
  async mounted() {
    const all = await this.$axios.$get("https://corona.lmao.ninja/all");
    this.all[0].count = all.cases;
    this.all[1].count = all.deaths;
    this.all[2].count = all.recovered;
  }
};
</script>