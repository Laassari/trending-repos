<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from './pages/home'
export default {
  name: 'app',
  components: {
    Home,
  },
}
</script>

<style>
body {
  font-size: 14px;
  color: #1f1f1f;
}

#app {
  max-width: 45rem;
  margin-left: auto;
  margin-right: auto;
  margin-top: 2rem;
}
</style>
