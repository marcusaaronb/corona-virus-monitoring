

<template>
  <div>
    <v-toolbar class="indigo lighten-1 white--text">
      <v-toolbar-title>Corona Virus Monitoring</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat icon dark @click="openGithub">
        <v-icon>public</v-icon>
      </v-btn>
    </v-toolbar>

    <v-container grid-list-md>
      <v-content>
        <v-layout>
          <v-flex xs12 sm4 v-for="all in all" :key="all.name">
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

    <!-- countries -->
    <v-container grid-list-md>
      <p>
        <v-text-field
          v-model="wholeWorld.dataIteratorConfig.search"
          label="Search..."
          :append-outer-icon="'search'"
        ></v-text-field>
      </p>

      <v-data-iterator
        :search="wholeWorld.dataIteratorConfig.search"
        :items="wholeWorld.countries"
        :rows-per-page-items="wholeWorld.dataIteratorConfig.rowsPerPageItems"
        :pagination.sync="wholeWorld.dataIteratorConfig.pagination"
        content-tag="v-layout"
        row
        wrap
      >
        <template v-slot:header>
          <v-toolbar class="mb-2" color="indigo darken-5" dark flat>
            <v-toolbar-title>Countries</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn flat icon @click="refreshWorld">
              <v-icon>refresh</v-icon>
            </v-btn>
          </v-toolbar>
        </template>
        <template v-slot:item="props">
          <v-flex xs12 sm6 md4 lg3>
            <v-card>
              <v-card-title>
                <h4>{{ props.item.country }}</h4>
                <v-spacer></v-spacer>
                <social-sharing
                  url="https://corona-virus-monitoring.herokuapp.com/"
                  :title="props.item.country"
                  :description="
                  `
                    Country:      ${props.item.country}
                    Cases:        ${props.item.todayCases}
                    Today Cases:  ${props.item.todayDeaths}
                    Deaths:       ${props.item.deaths}
                    Recovered:    ${props.item.recovered}
                    Active:       ${props.item.active}
                    Critical:     ${props.item.critical}
                  `
                  "
                  :quote="
                  `
                    Country:      ${props.item.country}
                    Cases:        ${props.item.todayCases}
                    Today Cases:  ${props.item.todayDeaths}
                    Deaths:       ${props.item.deaths}
                    Recovered:    ${props.item.recovered}
                    Active:       ${props.item.active}
                    Critical:     ${props.item.critical}
                  `
                  "
                  hashtags="covid-19,covid-monitoring"
                  inline-template
                >
                  <div>
                    <network network="facebook">
                      <v-btn icon small color="blue">
                        <v-tooltip bottom>
                          <v-icon color="white" small slot="activator">share</v-icon>
                          <span>Facebook Share</span>
                        </v-tooltip>
                      </v-btn>
                    </network>
                  </div>
                </social-sharing>
              </v-card-title>
              <v-divider></v-divider>
              <v-list dense>
                <v-list-tile>
                  <v-list-tile-content>Cases:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.cases }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Today Cases:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.todayCases }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Deaths:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.deaths }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Recovered:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.recovered }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Active:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.active }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Critical:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.critical }}</v-list-tile-content>
                </v-list-tile>
              </v-list>
            </v-card>
          </v-flex>
        </template>
      </v-data-iterator>
    </v-container>

    <v-container>
      <v-divider></v-divider>
    </v-container>

    <!-- states -->
    <v-container grid-list-md>
      <p>
        <v-text-field
          v-model="state.dataIteratorConfig.search"
          label="Search..."
          :append-outer-icon="'search'"
        ></v-text-field>
      </p>

      <v-data-iterator
        :search="state.dataIteratorConfig.search"
        :items="state.data"
        :rows-per-page-items="state.dataIteratorConfig.rowsPerPageItems"
        :pagination.sync="state.dataIteratorConfig.pagination"
        content-tag="v-layout"
        row
        wrap
      >
        <template v-slot:header>
          <v-toolbar class="mb-2" color="indigo darken-5" dark flat>
            <v-toolbar-title>USA</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn flat icon @click="refreshState">
              <v-icon>refresh</v-icon>
            </v-btn>
          </v-toolbar>
        </template>
        <template v-slot:item="props">
          <v-flex xs12 sm6 md4 lg3>
            <v-card>
              <v-card-title>
                <h4>{{ props.item.state }}</h4>
                <v-spacer></v-spacer>
                <social-sharing
                  url="https://corona-virus-monitoring.herokuapp.com/"
                  :title="props.item.state"
                  :description="
                  `
                    City:           ${props.item.state}
                    Cases:          ${props.item.cases}
                    Today Cases:    ${props.item.todayCases}
                    Deaths:         ${props.item.deaths}
                    Today Deaths:   ${props.item.todayDeaths}
                    Recovered:      ${props.item.recovered}
                    Active:         ${props.item.active}
                  `
                  "
                  :quote="
                  `
                    City:           ${props.item.state}
                    Cases:          ${props.item.cases}
                    Today Cases:    ${props.item.todayCases}
                    Deaths:         ${props.item.deaths}
                    Today Deaths:   ${props.item.todayDeaths}
                    Recovered:      ${props.item.recovered}
                    Active:         ${props.item.active}
                  `
                  "
                  hashtags="covid-19,covid-monitoring"
                  inline-template
                >
                  <div>
                    <network network="facebook">
                      <v-btn icon small color="blue">
                        <v-tooltip bottom>
                          <v-icon color="white" small slot="activator">share</v-icon>
                          <span>Facebook Share</span>
                        </v-tooltip>
                      </v-btn>
                    </network>
                  </div>
                </social-sharing>
              </v-card-title>
              <v-divider></v-divider>
              <v-list dense>
                <v-list-tile>
                  <v-list-tile-content>Cases:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.cases }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Today Cases:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.todayCases }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Deaths:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.deaths }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Today Deaths:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.todayDeaths }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Recovered:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.recovered }}</v-list-tile-content>
                </v-list-tile>
                <v-list-tile>
                  <v-list-tile-content>Active:</v-list-tile-content>
                  <v-list-tile-content style="align-items:flex-end">{{ props.item.active }}</v-list-tile-content>
                </v-list-tile>
              </v-list>
            </v-card>
          </v-flex>
        </template>
      </v-data-iterator>
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

        <v-card-text class="white--text">
          &copy;{{ new Date().getFullYear() }} —
          <strong>Marcus Aaron Baga</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </div>
</template>

<script>
let SocialSharing;
if (process.browser) {
  SocialSharing = require("vue-social-sharing");
}

export default {
  data: () => ({
    all: [
      {
        name: "Total Cases",
        count: 0,
        color: "blue"
      },
      {
        name: "Total Deaths",
        count: 0,
        color: "red"
      },
      {
        name: "Total Recovered",
        count: 0,
        color: "green"
      }
    ],
    wholeWorld: {
      is_loading: false,
      countries: [],
      dataIteratorConfig: {
        search: "",
        rowsPerPageItems: [8, 16, 32, 500],
        pagination: {
          rowsPerPage: 8
        }
      }
    },
    state: {
      data: [],
      dataIteratorConfig: {
        search: "",
        rowsPerPageItems: [8, 16, 32, 500],
        pagination: {
          rowsPerPage: 8
        }
      }
    }
  }),
  components: {
    "social-sharing": SocialSharing
  },
  async mounted() {
    const all = await this.$axios.$get("https://corona.lmao.ninja/all");
    this.all[0].count = all.cases;
    this.all[1].count = all.deaths;
    this.all[2].count = all.recovered;

    const countries = await this.$axios.$get(
      "https://corona.lmao.ninja/countries"
    );
    this.wholeWorld.countries = countries;

    const state = await this.$axios.$get("https://corona.lmao.ninja/states");
    this.state.data = state;
  },
  methods: {
    openGithub() {
      window.open(
        "https://github.com/marcusaaronb/corona-virus-monitoring",
        "_blank"
      );
    },
    async refreshWorld() {
      const countries = await this.$axios.$get(
        "https://corona.lmao.ninja/countries"
      );
      this.wholeWorld.countries = countries;
    },
    async refreshState() {
      const state = await this.$axios.$get("https://corona.lmao.ninja/states");
      this.state.data = state;
    }
  }
};
</script>

