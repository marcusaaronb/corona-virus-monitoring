<template>
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
          <v-card v-ripple @click="showHistory(props.item.country)">
            <v-card-title>
              <h4>
                <v-img :src="props.item.countryInfo.flag" height="50px" width="100px"></v-img>
                {{ props.item.country }}
              </h4>
              <v-spacer></v-spacer>
              <social-sharing
                url="https://corona-virus-monitoring.herokuapp.com/"
                :title="props.item.country"
                :description="
                  `
                    Country:      ${props.item.country}
                    Cases:        ${props.item.cases}
                    Today Cases:  ${props.item.todayCases != 0 ? '+ ' + props.item.todayCases : 0 }
                    Deaths:       ${props.item.deaths}
                    Today Deaths: ${props.item.todayDeaths != 0 ? '+ ' + props.item.todayDeaths : 0}
                    Recovered:    ${props.item.recovered}
                    Active:       ${props.item.active}
                    Critical:     ${props.item.critical}
                  `
                  "
                :quote="
                  `
                    Country:      ${props.item.country}
                    Cases:        ${props.item.cases}
                    Today Cases:  ${props.item.todayCases != 0 ? '+ ' + props.item.todayCases : 0 }
                    Deaths:       ${props.item.deaths}
                    Today Deaths: ${props.item.todayDeaths != 0 ? '+ ' + props.item.todayDeaths : 0}
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
                <v-list-tile-content
                  style="align-items:flex-end"
                >{{ props.item.todayCases != 0 ? '+ ' + props.item.todayCases : 0 }}</v-list-tile-content>
              </v-list-tile>
              <v-list-tile>
                <v-list-tile-content>Deaths:</v-list-tile-content>
                <v-list-tile-content style="align-items:flex-end">{{ props.item.deaths }}</v-list-tile-content>
              </v-list-tile>
              <v-list-tile>
                <v-list-tile-content>Today Deaths:</v-list-tile-content>
                <v-list-tile-content
                  style="align-items:flex-end"
                >{{ props.item.todayDeaths != 0 ? '+ ' + props.item.todayDeaths : 0 }}</v-list-tile-content>
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

    <!-- dialog -->
    <v-dialog v-model="dialog" width="400">
      <v-card>
        <v-card-title
          class="indigo lighten-1 white--text"
          primary-title
        >Historical | {{ history.country || 'N/A' }}</v-card-title>

        <v-tabs color="indigo lighten-2" dark slider-color="yellow">
          <v-tab ripple>Cases</v-tab>
          <v-tab-item>
            <v-card flat>
              <v-card-text
                v-for="(data, index) in history.timeline.cases"
                :key="index"
              >{{index}} - {{ data }}</v-card-text>
            </v-card>
          </v-tab-item>

          <v-tab ripple>Deaths</v-tab>
          <v-tab-item>
            <v-card flat>
              <v-card-text
                v-for="(data, index) in history.timeline.deaths"
                :key="index"
              >{{index}} - {{ data }}</v-card-text>
            </v-card>
          </v-tab-item>

          <v-tab ripple>Recovered</v-tab>
          <v-tab-item>
            <v-card flat>
              <v-card-text
                v-for="(data, index) in history.timeline.recovered"
                :key="index"
              >{{index}} - {{ data }}</v-card-text>
            </v-card>
          </v-tab-item>
        </v-tabs>
        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" flat @click="dialog = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
let SocialSharing;
if (process.browser) {
  SocialSharing = require("vue-social-sharing");
}

export default {
  data: () => ({
    dialog: false,
    wholeWorld: {
      is_loading: false,
      countries: [],
      dataIteratorConfig: {
        search: "",
        rowsPerPageItems: [8, 16, 32],
        pagination: {
          rowsPerPage: 8
        }
      }
    },
    history: {
      standardizedCountryName: null,
      timeline: {
        cases: null,
        deaths: null,
        recovered: null
      }
    }
  }),
  components: {
    "social-sharing": SocialSharing
  },
  async mounted() {
    const countries = await this.$axios.$get(
      "https://corona.lmao.ninja/v2/countries"
    );
    this.wholeWorld.countries = countries;
  },
  methods: {
    async refreshWorld() {
      const countries = await this.$axios.$get(
        "https://corona.lmao.ninja/v2/countries"
      );
      this.wholeWorld.countries = countries;
    },
    async showHistory(country) {
      const data = await this.$axios.$get(
        `https://corona.lmao.ninja/v2/historical/${country}`
      );
      this.history = data;
      this.dialog = true;
    }
  }
};
</script>