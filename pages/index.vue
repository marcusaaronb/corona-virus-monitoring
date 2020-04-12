

<template>
  <div>
    <!-- toolbar -->
    <toolbar />

    <!-- main -->
    <dashboard />

    <!-- countries -->
    <country />

    <v-container>
      <v-divider></v-divider>
    </v-container>

    <!-- ph cases -->
    <ph_covid_cases />

    <v-container>
      <v-divider></v-divider>
    </v-container>

    <!-- states -->
    <state />

    <!-- map -->
    <v-container>
      <div id="map" style="height: 100vh;border: 1px solid #AAA;"></div>
    </v-container>

    <!-- footer -->
    <footer_main />
  </div>
</template>

<script>
export default {
  data: () => ({
    data: []
  }),
  components: {
    toolbar: () =>
      import(/* webpackPrefetch: true */ "../components/toolbar.vue"),
    footer_main: () =>
      import(/* webpackPrefetch: true */ "../components/footer_main.vue"),
    dashboard: () =>
      import(
        /* webpackPrefetch: true */ "../components/dashboard/dashboard.vue"
      ),
    country: () =>
      import(/* webpackPrefetch: true */ "../components/dashboard/country.vue"),
    state: () =>
      import(/* webpackPrefetch: true */ "../components/dashboard/state.vue"),
    ph_covid_cases: () =>
      import(
        /* webpackPrefetch: true */ "../components/dashboard/ph_covid_cases.vue"
      )
  },
  async mounted() {
    const data = await this.$axios.$get("https://corona.lmao.ninja/v2/jhucsse");
    this.data = data;

    const map = this.$L.map("map", {
      center: [data[0].coordinates.latitude, data[0].coordinates.longitude],
      minZoom: 2,
      zoom: 13
    });

    const myIcon = L.icon({
      iconUrl:
        "http://www.clker.com/cliparts/b/7/6/5/1308001441853739087google%20maps%20pin.svg.med.png",
      iconRetinaUrl:
        "http://www.clker.com/cliparts/b/7/6/5/1308001441853739087google%20maps%20pin.svg.med.png",
      iconSize: [50, 34],
      iconAnchor: [9, 21],
      popupAnchor: [0, -14]
    });

    this.$L
      .tileLayer("http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>',
        subdomains: ["a", "b", "c"]
      })
      .addTo(map);

    this.data.forEach(e => {
      let latitude = e.coordinates.latitude;
      let longitude = e.coordinates.longitude;
      let country = e.country;
      let province = e.province == null ? "N/A" : e.province;
      let confirmed = e.stats.confirmed;
      let deaths = e.stats.deaths;
      let recovered = e.stats.recovered;
      let updatedAt = e.updatedAt;

      if (latitude != null && longitude != null) {
        this.$L
          .marker([latitude, longitude], {
            icon: myIcon
          })
          .bindPopup(
            "Country: " +
              country +
              "<br>" +
              "Province: " +
              province +
              "<br><br>" +
              "<b>Stats</b>" +
              "<br>" +
              "Confirmed: " +
              confirmed +
              "<br>" +
              "Deaths: " +
              deaths +
              "<br>" +
              "Recovered: " +
              recovered +
              "<br>" +
              "Updated At:" +
              updatedAt +
              "<br>" +
              "[Lat: " +
              latitude +
              ", Lon: " +
              longitude +
              "]"
          )
          .addTo(map);
      }
    });
  }
};
</script>

