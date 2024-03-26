<template>
  <div class="nav">
    <div class="header">
      <router-link :style="getRouterLinkStyles(0)" @click.native="changeNav(0)" to="/">Home</router-link>
      <router-link :style="getRouterLinkStyles(1)" @click.native="changeNav(1)" to="/chats">Chats</router-link>
      <router-link :style="getRouterLinkStyles(2)" @click.native="changeNav(2)" to="/users">Users</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  props: ['startingIndex'],
  data: () => {
    return {
      selectedIndex: 0
    }
  },
  mounted() {
    this.selectedIndex = this.startingIndex
  },
  methods: {
    getRouterLinkStyles(index) {
      return this.selectedIndex === index ? { borderBottom: '5px solid darkgreen' } : { borderBottom: '5px solid transparent' }
    },
    changeNav(index) {
      this.selectedIndex = index
    }
  }
}
</script>

<style scoped>
.nav {
  display: flex;
  background: green;
  padding-left: 1rem;
  align-items: center;
  padding-top: 1rem;
  padding-bottom: 1rem;
}

.header {
  background: green;
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-top: .7rem;
}

a {
  color: white;
  text-decoration: none;
  padding-bottom: .2rem;
  
}

a:hover {
  border-bottom: 5px solid darkgreen !important;
}
</style>