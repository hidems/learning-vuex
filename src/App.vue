<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
    <button @click="setLogin">Show Lgoin Name</button>
    {{ $store.state.count }}
    <br>

    <ul>
      <li v-for="user in visibleUsers" :key="user.id">
        {{ user.id }} - {{ user.name }} - {{ user.isVisible }}
      </li>
    </ul>
    <br>

    {{ getUserById }}
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'App',
  methods: {
    ...mapActions('auth', ['setLoginUser']),
    setLogin() {
      this.setLoginUser({name: 'Taro'})
    }
  },
  computed: {
    visibleUsers() {
      return this.$store.getters.visibleUsers
    },
    getUserById() {
      return this.$store.getters.getUserById(2)
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
