<template>
    <div class="card">
      <img :src="photo.url" alt="splash_image"/>
      <div class="card-body">
        <p>{{photo.label}}</p>
      </div>
      <button class="del-btn" @click="$emit('del-photo', photo)">Delete</button>
    </div>
</template>

<script>
export default {
  name: 'PhotoList',
  props: ['photo'],
  emits: ['del-photo']
}
</script>

<style>
</style>