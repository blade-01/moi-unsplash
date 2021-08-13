<template>
  <div class="add-photo">
    <button class="btn" @click="this.$emit('show-modal')">Add a photo</button>
  </div>
</template>

<script>
export default {
  name: 'AddPhoto',
  emits: ['show-modal'],
  data() {
    return {
    }
  },
  methods: {
  }
}
</script>

<style scoped>
.add-photo {
  margin-top: 1rem;
}
@media screen and (min-width: 700px) {
  .add-photo {
    margin: 0;
  }
}
</style>