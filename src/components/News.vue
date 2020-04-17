<template>
  <div class="container">
    <h1>Utilisation de l'API de Drupal 8 - contenu "actualités"</h1>
    <b-carousel
      id="carousel-1"
      v-model="slide"
      :interval="4000"
      controls
      indicators
      background="#ababab"
      style="text-shadow: 1px 1px 2px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      <b-carousel-slide v-for="(actualite, index) in actualites" :key="index">
        <h3>{{ actualite.title[0].value }}</h3>
        <template v-slot:img>
          <img
            class="d-block img-fluid w-100"
            width="1024"
            height="480"
            :src="actualite.field_image[0].url"
            :alt="actualite.field_image[0].alt"
          />
        </template>
      </b-carousel-slide>
    </b-carousel>

    <div class="row">
      <b-card v-for="(actualite, index) in actualites" :key="index" class="col-4">
        <b-card-img :src="actualite.field_image[0].url" :alt="actualite.field_image[0].alt"></b-card-img>
        <b-card-text>{{ actualite.title[0].value }}</b-card-text>

        <b-button href="#" variant="primary">Lire plus</b-button>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  name: "News",
  data() {
    return {
      url: "http://d8-base.test/api/news?_format=json",
      actualites: [],
      slide: 0,
      sliding: null
    };
  },
  props: {
    msg: String
  },
  mounted() {
    this.axios
      .get(this.url)
      .then(actualites => (this.actualites = actualites.data));
  },
  methods: {
    onSlideStart() {
      this.sliding = true;
    },
    onSlideEnd() {
      this.sliding = false;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
