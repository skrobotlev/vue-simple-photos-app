<template>
  <v-container>
    <!--     <Photo v-for="photo in photos" v-bind:photo="photo" /> -->
    <!-- <PhotoForm v-show="dialogsVisible" @addPhoto="addPhoto" /> -->
    <PhotoForm v-if="photos.length < 11" @addPhoto="addPhoto" />
    <div v-else>You Cannot add photos</div>
    <v-row>
      <Photo @openPhoto="openPhoto" v-for="photo in photos" :photo="photo" />
    </v-row>
    <PhotoDialog :photo="currentPhoto" v-model="dialogVisible" />
  </v-container>
</template>

<script>
import Photo from "@/components/photo/Photo";
import PhotoForm from "@/components/photo/PhotoForm";
import PhotoDialog from "@/components/photo/PhotoDialog";
export default {
  components: { Photo, PhotoForm, PhotoDialog },
  data: () => ({
    photos: [],
    currentPhoto: {},
    dialogVisible: false,
  }),
  mounted() {
    this.fetchTodo();
  },
  methods: {
    fetchTodo() {
      this.axios
        .get(`https://jsonplaceholder.typicode.com/photos?_limit=10`)
        .then((res) => (this.photos = res.data));
    },
    addPhoto(photo) {
      this.photos.push(photo);
    },
    openPhoto(photo) {
      this.currentPhoto = photo;
      this.dialogVisible = true;
    },
  },
};
</script>

<style></style>
