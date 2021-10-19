<template>
<link href="https://allfont.net/allfont.css?fonts=star-jedi" rel="stylesheet" type="text/css" />
<search-page></search-page>
</template>

<script>
import SearchPage from './components/SearchPage.vue'

export default {
  name: 'App',
  components: {
    SearchPage
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;300;400;500&display=swap');

body {
  margin: 0;
  display: flex;
}

#app {
  font-family: 'Montserrat', sans-serif;
  width: 100%;
}

h1 {
  font-family: 'Star Jedi', arial;
}

</style>
