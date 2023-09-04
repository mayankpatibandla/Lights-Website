<template>
  <div id="app">
    <div class="header">
      <div data-netlify-identity-menu></div>
    </div>
    <div v-if="isLoggedIn">
      <div><a href="https://google.com">ISLOGGEDIN!!!</a></div>
    </div>
    <div v-else><h1>NOT LOGGED IN!!!</h1></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'App',
  data() {
    return {
      isLoggedIn: false,
      token: ''
    }
  },
  async created() {
    // eslint-disable-next-line @typescript-eslint/no-this-alias
    const self = this

    // eslint-disable-next-line no-undef, @typescript-eslint/no-explicit-any
    netlifyIdentity.on('init', async (user: any) => {
      if (user) {
        self.token = user.token.access_token
        self.isLoggedIn = true
      }
    })

    // eslint-disable-next-line no-undef
    netlifyIdentity.on('login', (user: { token: { access_token: string } }) => {
      self.token = user.token.access_token
      self.isLoggedIn = true
    })

    // eslint-disable-next-line no-undef
    netlifyIdentity.on('logout', () => {
      self.token = ''
      self.isLoggedIn = false
    })
  }
})
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
