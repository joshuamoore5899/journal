<template>
<div class="main">
  <div class="menu">
    <h2><a @click="toggleUpload">New Entry <i class="fas fa-book"></i></a></h2>
    <h2>{{user.firstName}} {{user.lastName}} | Logout <a @click="logout"><i class="fas fa-sign-out-alt"></i></a></h2>
    <uploader :show="show" @close="close" @uploadFinished="uploadFinished" />
  </div>
  <p v-if="error">{{error}}</p>
</div>
</template>

<script>
import axios from 'axios';
import Uploader from '@/components/Uploader.vue';
export default {
  name: 'MyPhotos',
  components: {
    Uploader,
  },
  data() {
    return {
      show: false,
      photos: [],
      error: '',
    }
  },
  created() {
    this.getPhotos();
  },
  computed: {
    user() {
      return this.$root.$data.user;
    },
  },
  methods: {
    async logout() {
      try {
        await axios.delete("/api/users");
        this.$root.$data.user = null;
      } catch (error) {
        this.$root.$data.user = null;
      }
    },
    async getPhotos() {
      try {
        this.response = await axios.get("/api/photos");
        this.photos = this.response.data;
      } catch (error) {
        this.error = error.response.data.message;
      }
    },
    close() {
      this.show = false;
    },
    toggleUpload() {
      this.show = true;
    },
    async uploadFinished() {
      this.show = false;
      this.getPhotos();
    },
  }
}
</script>

<style scoped>
.menu {
  display: flex;
  justify-content: space-between;
}

.menu h2 {
  font-size: 14px;
}

.main-content {
  display: flex;
  justify-content: center;
}
</style>
