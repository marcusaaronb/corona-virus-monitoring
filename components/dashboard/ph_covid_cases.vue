<template>
  <v-container>
    <p>
      <v-text-field v-model="search" label="Search..." :append-outer-icon="'search'"></v-text-field>
    </p>
    <v-card>
      <v-card-title primary-title class="indigo lighten-1 white--text">
        <div class="headline">Philippines Cases</div>
        <v-spacer></v-spacer>
        <v-btn flat icon @click="refreshPhCovid" dark>
          <v-icon>refresh</v-icon>
        </v-btn>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="data"
        :loading="loading"
        :search="search"
        class="elevation-1"
      >
        <template v-slot:items="props">
          <td>{{ props.item.case_no || 'N/A' }}</td>
          <td class="text-xs-right">{{ props.item.date || 'N/A' }}</td>
          <td>{{ props.item.age || 'N/A' }}</td>
          <td class="text-xs-right">{{ props.item.gender == 'F' ? 'Female' : 'Male' || 'N/A'}}</td>
          <td class="text-xs-right">{{ props.item.nationality || 'N/A' }}</td>
          <td class="text-xs-right">{{ props.item.hospital_admitted_to || 'N/A' }}</td>
          <td class="text-xs-right">{{ props.item.had_recent_travel_history_abroad || 'N/A' }}</td>
          <td class="text-xs-right">{{ props.item.status || 'N/A' }}</td>
          <td class="text-xs-right">{{ props.item.other_information || 'N/A'}}</td>
        </template>
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    loading: false,
    headers: [
      {
        text: "Cases #",
        align: "left",
        sortable: false,
        value: "case_no"
      },
      { text: "Date", value: "date" },
      { text: "Age", value: "age", align: "left" },
      { text: "Gender", value: "gender" },
      { text: "Nationality", value: "nationality" },
      { text: "Hospital Admiited", value: "hospital_admitted_to" },
      {
        text: "Travel History",
        value: "had_recent_travel_history_abroad"
      },
      { text: "Status", value: "status" },
      { text: "Other Info", value: "other_information" }
    ],
    data: [],
    search: ""
  }),
  async mounted() {
    this.loading = true;
    const data = await this.$axios.$get(
      "https://coronavirus-ph-api.now.sh/cases"
    );
    this.data = data;
    this.loading = false;
  },
  methods: {
    async refreshPhCovid() {
      this.loading = true;
      const data = await this.$axios.$get(
        "https://coronavirus-ph-api.now.sh/cases"
      );
      this.data = data;
      this.loading = false;
    }
  }
};
</script>