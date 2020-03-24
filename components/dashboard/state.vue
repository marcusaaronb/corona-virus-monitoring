<template>
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
                    Today Cases:    ${props.item.todayCases != 0 ? '+ ' + props.item.todayCases : 0}
                    Deaths:         ${props.item.deaths}
                    Today Deaths:   ${props.item.todayDeaths != 0 ? '+ ' + props.item.todayDeaths : 0 }
                    Recovered:      ${props.item.recovered}
                    Active:         ${props.item.active}
                  `
                  "
                :quote="
                  `
                    City:           ${props.item.state}
                    Cases:          ${props.item.cases}
                    Today Cases:    ${props.item.todayCases != 0 ? '+ ' + props.item.todayCases : 0}
                    Deaths:         ${props.item.deaths}
                    Today Deaths:   ${props.item.todayDeaths != 0 ? '+ ' + props.item.todayDeaths : 0 }
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
            </v-list>
          </v-card>
        </v-flex>
      </template>
    </v-data-iterator>
  </v-container>
</template>

<script>
let SocialSharing;
if (process.browser) {
  SocialSharing = require("vue-social-sharing");
}

export default {
  data: () => ({
    state: {
      data: [],
      dataIteratorConfig: {
        search: "",
        rowsPerPageItems: [8, 16, 32],
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
    const state = await this.$axios.$get("https://corona.lmao.ninja/states");
    this.state.data = state;
  },
  methods: {
    async refreshState() {
      const state = await this.$axios.$get("https://corona.lmao.ninja/states");
      this.state.data = state;
    }
  }
};
</script>