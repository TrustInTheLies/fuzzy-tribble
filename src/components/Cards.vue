<template>
  <v-row>
    <v-col
      v-for="image in images"
      :key="image.id"
      class="d-flex"
      cols="4"
      @click="getImage(image.id)"
    >
      <v-img :src="image.url" :id="image.id">
        <template v-slot:placeholder>
          <v-row class="fill-height ma-0" align="center" justify="center">
            <v-progress-circular
              indeterminate
              color="grey lighten-5"
            ></v-progress-circular>
          </v-row>
        </template>
      </v-img>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "Cards",
  props: ["images"],
  data: () => ({
    imageProps: {},
  }),
  methods: {
    getImage(imageId) {
      fetch(`https://boiling-refuge-66454.herokuapp.com/images/${imageId}`)
        .then((res) => {
          if (res.status == 200) {
            return res.json();
          } else {
            throw new Error(res.status);
          }
        })
        .then((data) => {
          this.$emit("addImage", data);
        });
    },
  },
};
</script>

<style></style>
