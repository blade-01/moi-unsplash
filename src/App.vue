<template>
  <div class="container">
    <Main />
  </div>
</template>

<script>
import Main from '@/components/Main.vue'

export default {
  name: 'App',
  components: {Main},
}
</script>

<style>
:root {
  --text: #333333;
  --bg: #ffffff;
  --btn: #3db46d;
  --form: #BDBDBD;
  --del-btn: #EB5757;
  --add-form: #4F4F4F;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: var(--bg);
  color: var(--text);
}
*,
*::before,
*::after {
  box-sizing: border-box;
}
.container {
  width: 90%;
  overflow: hidden;
  margin: auto;
}
form input {
  padding: 0.8rem 2rem;
  display: block;
  width: 100%;
  border-radius: 5px;
  border: solid 1px var(--form);
  color: var(--text);
  outline: none;
}
form input::placeholder {
  color: var(--form);
}
svg,
button {
  cursor: pointer;
}
img {
  width: 100%;
  border-radius: 10px;
}
.btn {
  padding: 0.8rem;
  display: block;
  border-radius: 5px;
  border: none;
  background: var(--btn);
  color: var(--bg);
  outline: none;
  font-weight: bold;
}
.btn-shadow {
  box-shadow: 0 3px 3px 0 rgba(0, 0, 0, 0.14);
}
@media screen and (min-width: 700px) {
 .container {
    width: 650px;
  }
}
@media screen and (min-width: 1000px) {
 .container {
    width: 900px;
  }
}
@media screen and (min-width: 1200px) {
 .container {
    width: 1200px;
  }
}
</style>
