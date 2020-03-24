<template>
  <div>
    <toolbar />

    <v-container>
      <v-card>
        <v-container grid-list-md fluid>
          <v-layout row wrap>
            <v-flex v-for="helpfulImage in helpfulImage" :key="helpfulImage.img_src" xs4 d-flex>
              <v-card flat tile class="d-flex">
                <v-img
                  :key="helpfulImage.img_src"
                  :src="helpfulImage.img_src"
                  :lazy-src="helpfulImage.img_src"
                  @click="openImage(helpfulImage.img_src)"
                  aspect-ratio="1"
                  class="grey lighten-2"
                  large
                  style="cursor:pointer"
                >
                  <template v-slot:placeholder>
                    <v-layout fill-height align-center justify-center ma-0>
                      <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                    </v-layout>
                  </template>
                </v-img>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card>
    </v-container>

    <footer_main />
  </div>
</template>

<script>
export default {
  data: () => ({
    helpfulImage: [
      {
        img_src:
          "https://scontent.fmnl17-1.fna.fbcdn.net/v/t1.0-9/p960x960/89987075_3152714258073138_1927950874315849728_o.png?_nc_cat=106&_nc_sid=8024bb&_nc_ohc=oG7Sx3EU8LQAX8dvbnk&_nc_ht=scontent.fmnl17-1.fna&oh=65617b533ad93a9bc68681a58413c8c4&oe=5E9D8A56"
      },
      {
        img_src:
          "https://scontent.fmnl17-1.fna.fbcdn.net/v/t1.15752-9/90509616_575882276619034_5895502196182614016_n.jpg?_nc_cat=104&_nc_sid=b96e70&_nc_eui2=AeHxE4mhAS13uO0I-7XuH_8DZkMQTFe-lsCAIGfZK_b-t7vciM2P0vQSVqZ3s3Nr76pXY_rRhhkDbRT7vdRR2en0K5cBpA771W1Z66WzLad77Q&_nc_ohc=VjXfkowbNjgAX_PMOJO&_nc_ht=scontent.fmnl17-1.fna&oh=7ce681d1ac8fc371c33cbfe666889c9b&oe=5E9E0DAB"
      },
      {
        img_src:
          "https://scontent.fmnl17-2.fna.fbcdn.net/v/t1.0-9/p960x960/90589012_3169371486407415_2928529674185211904_o.jpg?_nc_cat=103&_nc_sid=8024bb&_nc_ohc=ktZavYck-CgAX_tbscF&_nc_ht=scontent.fmnl17-2.fna&_nc_tp=6&oh=dbf06c795f13ba23ffde0ff7a8df9a40&oe=5E9F7577"
      },
      {
        img_src:
          "https://scontent.fmnl17-2.fna.fbcdn.net/v/t1.0-9/p960x960/90227270_102857478032109_3887209938505695232_o.png?_nc_cat=102&_nc_sid=8024bb&_nc_ohc=TmfWUYa4Z7gAX-h7hFT&_nc_ht=scontent.fmnl17-2.fna&oh=0f3051963278dc5f2569d1ee725f1202&oe=5EA0444F"
      },
      {
        img_src:
          "https://scontent.fmnl17-1.fna.fbcdn.net/v/t1.0-9/90373649_1649725235166606_6124489206497542144_n.jpg?_nc_cat=1&_nc_sid=110474&_nc_ohc=_9jQM16C4ckAX9wu33z&_nc_ht=scontent.fmnl17-1.fna&oh=e8b13a00535f480e4bc5a0d63f03be98&oe=5EA000C2"
      },
      {
        img_src:
          "https://scontent.fmnl17-1.fna.fbcdn.net/v/t1.0-9/90244460_1649725378499925_2415129083420606464_n.jpg?_nc_cat=105&_nc_sid=110474&_nc_ohc=WCNaAHANTLQAX_xjpHC&_nc_ht=scontent.fmnl17-1.fna&oh=364794cf90a42024e6bfddc07da202db&oe=5E9D49F8"
      },
      {
        img_src:
          "https://scontent.fmnl17-1.fna.fbcdn.net/v/t1.0-9/s960x960/90114903_3162497827094781_720535189729574912_o.jpg?_nc_cat=1&_nc_sid=8024bb&_nc_ohc=zlM6c-efb5oAX8epOYH&_nc_ht=scontent.fmnl17-1.fna&_nc_tp=7&oh=a2072e443e4657f6aa6b0b7e488ae957&oe=5EA01595"
      },
      {
        img_src:
          "https://scontent.fmnl17-1.fna.fbcdn.net/v/t1.0-9/p960x960/89972378_3162441847100379_9001715668130725888_o.jpg?_nc_cat=108&_nc_sid=8024bb&_nc_ohc=x3XJpNZ_O-4AX87-jay&_nc_ht=scontent.fmnl17-1.fna&_nc_tp=6&oh=2a4efe20974a4a346bcabc8487632213&oe=5E9D5FED"
      },
      {
        img_src:
          "https://scontent.fmnl17-1.fna.fbcdn.net/v/t1.0-9/90935275_3162431917101372_8067326424576425984_n.jpg?_nc_cat=108&_nc_sid=8024bb&_nc_ohc=zTOaUNbWfVYAX8jVL3g&_nc_ht=scontent.fmnl17-1.fna&oh=01b464422c9d8b6a0b8e3414eeeba63e&oe=5E9DF8D8"
      }
    ]
  }),
  components: {
    toolbar: () => import("../components/toolbar.vue"),
    footer_main: () => import("../components/footer_main.vue")
  },
  methods: {
    openImage(imgSrc) {
      window.open(imgSrc, "_blank");
    }
  }
};
</script>