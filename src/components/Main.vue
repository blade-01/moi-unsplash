<template>
  <header>
    <div class="flex-item">
      <img src="../assets/img/my_unsplash_logo.svg" alt="">
      <search-photo @search-photo="searchPhoto"/>
    </div>
    <add-photo @show-modal="showModal"/>
  </header>
    <form-modal @add-photo="addPhoto" @remove-modal="removeModal" v-show="modal"/>
    <Photos :photos="photos" @del-photo="deletePhoto"/>
</template>

<script>
import AddPhoto from '@/components/AddPhoto.vue'
import Photos from '@/components/Photos.vue'
import SearchPhoto from '@/components/SearchPhoto.vue'
import FormModal from '@/components/FormModal.vue'

export default {
  name: 'Header',
  components: {
    AddPhoto, 
    SearchPhoto,
    Photos,
    FormModal
  },
  data() {
    return {
      modal: false,
      photos: [
      {
        id: 0,
        url: 'https://i0.wp.com/www.seriezloaded.com.ng/wp-content/uploads/2021/03/wp-1614820269047.jpg?resize=678%2C1017&ssl=1',
        label: 'Mouse',
      },
      {
        id: 1,
        url: 'https://asianwiki.com/images/0/01/Vincenzo-KD-p1.jpg',
        label: 'Vincenzo',
      },
      {
        id: 2,
        url: 'https://thumbnails.kpopmap.com/2021/01/Sisyphus-The-Myth-cast-and-summary-cover-680x384.jpg',
        label: 'Sisyphus - The Myth'
      },
      {
        id: 3,
        url: 'https://upload.wikimedia.org/wikipedia/en/e/eb/Maher_Zain_Album_One.jpg',
        label: 'Maher Zain - One',
      },
      {
        id: 4,
        url: 'https://mcdn.wallpapersafari.com/medium/69/22/brlIHf.jpg',
        label: 'Death Note',
      },
      {
        id: 5,
        url: 'https://www.denofgeek.com/wp-content/uploads/2016/02/fast-9-poster-cast-universal.jpg?resize=768%2C432',
        label: 'Fast and Furious 9',
      },
    ]
    }
  },
  methods: {
    addPhoto(photo) {
      this.photos = [photo, ...this.photos];
      this.savePhoto();
    },
    showModal() {
      this.modal = !this.modal;
    },
    removeModal() {
      this.modal = false;
    },
    deletePhoto(photo) {
      this.photos.splice(this.photos.indexOf(photo), 1);
      this.savePhoto();
    },
    savePhoto() {
      localStorage.setItem('photos', JSON.stringify(this.photos))
    },
    // searchPhoto(photo) {
    //   this.photos.filter(pho => {
    //     pho.label.match(photo);
    //   });
    // }
  },
  mounted() {
    this.photos = JSON.parse(localStorage.getItem('photos') || JSON.stringify(this.photos));
  }
}
</script>

<style scoped>
header {
  padding: 1rem 0;
}
header img {
  width: 200px;
}
@media screen and (min-width: 700px) {
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  header img {
    width: 150px;
  }
  header .flex-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
}
</style>