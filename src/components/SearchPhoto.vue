<template>
  <div class="search-photo">
    <form>
      <input @keyup="searchPhoto" type="text" placeholder="Search by name" v-model="search">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SearchPhoto',
  emits: ['search-photo'],
  data() {
    return {
      search: '',
    }
  },
  methods: {
    searchPhoto() {
      this.$emit('search-photo', this.search);
    }
  }
}
</script>

<style scoped>
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
@media screen and (min-width: 700px) {
  .search-photo {
    margin: 0;
  }
  .search-photo form input {
    width: 220px;
  }
}
@media screen and (min-width: 1000px) {
  .search-photo form input {
    width: 300px;
  }
}
</style>