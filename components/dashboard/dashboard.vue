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
      <v-layout>
        <v-flex xs4 sm4 md4 v-for="all in all1" :key="all.name">
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
      <v-layout>
        <v-flex xs4 sm4 md4 v-for="all in all2" :key="all.name">
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
      <v-layout>
        <v-flex xs4 sm4 md4 v-for="all in all3" :key="all.name">
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
    ],
    all1: [
      {
        name: "Today Cases",
        count: 0,
        color: "blue"
      },
      {
        name: "Today Deaths",
        count: 0,
        color: "red"
      },
      {
        name: "Active",
        count: 0,
        color: "green"
      }
    ],
    all2: [
      {
        name: "Case Per 1M",
        count: 0,
        color: "blue"
      },
      {
        name: "Death Per 1M",
        count: 0,
        color: "red"
      },
      {
        name: "Test Per 1M",
        count: 0,
        color: "green"
      }
    ],
    all3: [
      {
        name: "Crtical",
        count: 0,
        color: "blue"
      },
      {
        name: "Tests",
        count: 0,
        color: "red"
      },
      {
        name: "Affected  Countries",
        count: 0,
        color: "green"
      }
    ]
  }),
  async mounted() {
    const all = await this.$axios.$get("https://corona.lmao.ninja/v2/all");
    this.all[0].count = all.cases;
    this.all[1].count = all.deaths;
    this.all[2].count = all.recovered;

    this.all1[0].count = all.todayCases;
    this.all1[1].count = all.todayDeaths;
    this.all1[2].count = all.active;

    this.all2[0].count = all.casesPerOneMillion;
    this.all2[1].count = all.deathsPerOneMillion;
    this.all2[2].count = all.testsPerOneMillion;

    this.all3[0].count = all.critical;
    this.all3[1].count = all.tests;
    this.all3[2].count = all.affectedCountries;
  }
};
</script>