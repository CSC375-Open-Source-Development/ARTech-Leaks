<template>
  <div id="app">
    <NavBar :startingIndex="startingIndex" />
    <router-view/>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'

export default {
  name: 'App',
  components: {
    NavBar
  },
  computed: {
    startingIndex() {
      switch (this.$route.name) {
        case 'Home':
          return 0
        case 'Chats':
        case 'Chat':
          return 1
        case 'About':
          return 2
        default:
          return -1
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

#app {
  font-family: 'Roboto', sans-serif
}

body {
  overflow-y: scroll
}
</style>
