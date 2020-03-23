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