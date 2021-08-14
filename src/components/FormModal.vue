<template>
  <div class="form-modal">
    <div class="form-modal-content">
      <form @submit.prevent="addPhoto">
        <div class="flex">
          <h4>Add a new photo</h4>
          <svg class="w-6 h-6 close" @click="this.$emit('remove-modal')" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
        </div>
        <small class="err" v-show="err">{{err}}</small>
        <div class="form-field">
          <label for="label">Label</label>
          <input type="text" id="label" placeholder="Mirabel Sanudai - Memorabilia" v-model="label">
        </div>
        <div class="form-field">
          <label for="url">Photo URL</label>
          <input type="text" id="url" placeholder="https://unsplash.com/sl13l" v-model="url">
        </div>
        <div class="form-field submit-field">
          <input type="submit" value="Submit" class="btn submit-btn btn-shadow">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FormModal',
  emits: ['remove-modal', 'add-photo'],
  data() {
    return {
      label: '',
      url: '',
      err: null,
    }
  },
  methods: {
    addPhoto() {
      const newPhoto = {
        id: Math.random(),
        url: this.url,
        label: this.label,
        
      };
      if (this.url == '' || this.label == '') {
        this.err = this.errMssg('Please fill all fields');
        setTimeout(() => {this.err = null}, 1500);
      } else if(this.label.length > 30) {
          this.err = this.errMssg('Characters too long');
          setTimeout(() => {this.err = null}, 1500);
      } else {
        this.$emit('add-photo', newPhoto);
        this.$emit('remove-modal')
        this.label = '';
        this.url = '';
      }
    },
    errMssg(mssg) {
      return mssg;
    }
  }
}
</script>

<style scoped>
.form-modal {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 10;
}
.form-modal-content {
  position: absolute;
  top: 15%;
  left: 50%;
  transform: translate(-50%, 0);
  background: var(--bg);
  padding: 0 1rem;
  border-radius: 5px;
  width: 90%;
}
.form-modal-content h4 {
  margin-bottom: 1rem;
}
.form-field {
  color: var(--add-form);
  margin: 1.3rem 0;
}
.form-field label {
  display: block;
  padding-bottom: 0.5rem;
}
.form-field input {
  padding: 0.8rem;
}
.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.flex svg {
  width: 25px;
}
.submit-field {
  display: flex;
  justify-content: flex-end;
}
.btn.submit-btn {
  width: auto;
  padding: 0.7rem 1rem;
}
small.err {
  display: block;
  width: 100%;
  padding: 0.8rem;
  border-radius: 5px;
  color: var(--del-btn);
  background: transparent;
  border: solid 1px var(--del-btn);
  text-align: center;
}
@media screen and (min-width: 700px) {
  .form-modal-content {
    width: 450px;
  }
}
</style>