<template>
  <v-app>
    <v-main>
      <h1 class="text-center text-uppercase">Gallery</h1>
      <Cards :images="images" @addImage="updateImage($event)" />
    </v-main>
  </v-app>
</template>

<script>
import Cards from "./components/Cards.vue";

export default {
  name: "App",

  components: { Cards },

  data: () => ({
    images: {},
    image: {},
  }),
  created() {
    fetch("https://boiling-refuge-66454.herokuapp.com/images")
      .then((res) => {
        if (res.status == 200) {
          return res.json();
        } else {
          console.log(res.status);
        }
      })
      .then((data) => {
        this.images = data;
      });
  },
  methods: {
    updateImage: function (updatedImage) {
      this.image = updatedImage;
    },
  },
};
</script>
