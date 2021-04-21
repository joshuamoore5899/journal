<template>
<div>
  <section class="image-gallery">
    <div class="image" v-for="photo in photos" v-bind:key="photo._id">
      <img :src="photo.path" />
      <p class="photoDate">{{formatDate(photo.created)}} was a(n) {{photo.title}} day</p>
      <div class="photoInfo">
        <p class="photoName">{{photo.description}}</p>
      </div>
    </div>
  </section>
</div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'ImageGallery',
  props: {
    photos: Array
  },
  methods: {
    formatDate(date) {
        return moment(date).format('MMMM DD, YYYY');
    }
  }
}
</script>

<style scoped>
.photoInfo {
  display: flex;
  justify-content: space-between;
  font-size: 1.2em;
}

.photoInfo p {
  margin: 20px;
}

.photoDate {
  font-size: 1.0em;
  font-weight: bold;
}

p {
  margin: 0px;
}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

.image-gallery {
  column-gap: 1em;
}

.image {
  flex-direction: column;
  align-items: center;
  margin: 0 0 1.5em;
  display: flex;
  justify-content: center;
  width: 100%;
}

.image img {
  width: 95%;
}

@media only screen and (min-width: 1024px) {
  .image img {
  width: 40%;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image img {
  width: 55%;
}
}
</style>
