<template>
  <header>
    <div class="flex-item">
      <img src="../assets/img/my_unsplash_logo.svg" alt="">
      <div class="search-photo">
        <form>
          <input type="text" placeholder="Search by name" v-model="search">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
        </form>
      </div>
    </div>
    <add-photo @show-modal="showModal"/>
  </header>
    <form-modal @add-photo="addPhoto" @remove-modal="removeModal" v-show="modal"/>
    <div class="cards">
      <div class="card" v-for="photo in searchPhoto" :key="photo.id">
        <img :src="photo.url" alt="splash_image"/>
        <div class="card-body">
          <p>{{photo.label}}</p>
        </div>
        <button class="del-btn" @click="deletePhoto(photo)">Delete</button>
      </div>
    </div>
</template>

<script>
import AddPhoto from '@/components/AddPhoto.vue'
import FormModal from '@/components/FormModal.vue'

export default {
  name: 'Header',
  components: {
    AddPhoto,
    FormModal
  },
  data() {
    return {
      modal: false,
      search: '',
      photos: [
      {
        id: 0,
        url: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTvXCvbtF-Il4K0KaIZAVHtgkWM88-zGg_QGw&usqp=CAU',
        label: 'Aesthetic Dicron',
      },
      {
        id: 1,
        url: 'https://asianwiki.com/images/0/01/Vincenzo-KD-p1.jpg',
        label: 'vincenzo',
      },
      {
        id: 2,
        url: 'https://i0.wp.com/www.seriezloaded.com.ng/wp-content/uploads/2021/03/wp-1614820269047.jpg?resize=678%2C1017&ssl=1',
        label: 'Mouse',
      },
      {
        id: 3,
        url: 'https://thumbnails.kpopmap.com/2021/01/Sisyphus-The-Myth-cast-and-summary-cover-680x384.jpg',
        label: 'Sisyphus - The Myth',
      },
      {
        id: 4,
        url: 'https://mcdn.wallpapersafari.com/medium/69/22/brlIHf.jpg',
        label: 'Death Note',
      },
      {
        id: 5,

        url: 'https://upload.wikimedia.org/wikipedia/en/e/eb/Maher_Zain_Album_One.jpg',
        label: 'Maher Zain - One',
      },
      {
        id: 6,
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
  },
  computed: {
    searchPhoto() {
      return this.photos.filter(photo => {
        return photo.label.toLowerCase().includes(this.search.toLowerCase());
      });
    }
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
.search-photo {
  margin-top: 1rem;
}
.search-photo form {
  position: relative;
}
.search-photo form svg {
  width: 20px;
  position: absolute;
  top: 50%;
  left: 10px;
  transform: translate(0, -50%);
}
.cards {
  margin-top: 1rem;
}
.cards .card img {
  width: 100%;
  border-radius: 10px;
}
.del-btn {
  padding: 0.5rem 1rem;
  border-radius: 50px;
  color: var(--del-btn);
  background: transparent;
  border: solid 1px var(--del-btn);
  text-align: center;
  position: absolute;
  top: 20px;
  right: 20px;
}
.card {
  position: relative;
  cursor: pointer;
}
.cards .card {
  margin-bottom: 0.75rem;
}
.cards .card .card-body p {
  font-weight: bold;
}
.cards .card .card-body {
  padding: 1rem;
  position: absolute;
  left: 0;
  bottom: 0;
  color: #fff;
  text-shadow: 0 1px 1px rgba(255, 255, 255, 0.4);
}
.del-btn {
  opacity: 0;
  transition: opacity 0.4s ease-in-out;
}
.card:hover .del-btn {
  opacity: 1;
}
.card:hover .card::after{
  content: '';
  position: absolute;
  height: 100%;
  width: 100%;
  box-shadow: inset 0px 3px 4px 4px rgba(0, 0, 0, 0.5);
  z-index: 1000;
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
  .search-photo {
    margin: 0;
  }
  .search-photo form input {
    width: 220px;
  }
  .cards {
    column-count: 3;
    column-gap: 1.25rem;
  }
  .cards .card {
    display: inline-block;
    width: 100%;
  }
}
@media screen and (min-width: 1000px) {
  .search-photo form input {
    width: 300px;
  }
  .cards {
    column-count: 3;
  }
}
</style>