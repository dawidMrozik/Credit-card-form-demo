<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from './components/form/Form.vue';

export default {
  name: 'App',
  components: {
    Form,
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Source+Code+Pro:400,500,600,700|Source+Sans+Pro:400,600,700&display=swap');

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
  background-color: lightblue;
}

#app {
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 16px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
