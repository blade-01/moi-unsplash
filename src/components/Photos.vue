<template>
  <div class="cards">
    <div class="photos" v-for="photo in photos" :key="photo.id">
      <photo-list :photo="photo" @del-photo="$emit('del-photo', photo)"/>
    </div>
  </div>
</template>

<script>
import PhotoList from '@/components/PhotoList.vue'
export default {
  name: 'Photos',
  props: ['photos'],
  emits: ['del-photo'],
  components: {PhotoList},
  data() {
    return {

    }
  }
}
</script>

<style>
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
@media screen and (min-width: 576px) {
  .cards {
    column-count: 2;
    column-gap: 1.25rem;
  }
  .cards .card {
    display: inline-block;
    width: 100%;
  }
}
@media screen and (min-width: 1000px) {
  .cards {
    column-count: 3;
  }
}
</style>