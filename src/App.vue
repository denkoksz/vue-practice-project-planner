<template>

  <navBar></navBar>
  <router-view/>
</template>

<script>
import NavBar from '@/components/Navbar'

export default {
  components: { NavBar }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}
button:hover {
  cursor: pointer;
}

</style>
