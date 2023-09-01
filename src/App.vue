<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <!--Login-->
  <div data-netlify-identity-button></div>

  <div v-if="isLoggedIn">
    <p>Secret Content</p>
  </div>
  <div v-else>
    <p>Not logged in!!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoggedIn: false
    }
  },
  async created() {
    // https://www.youtube.com/watch?v=uY1HTcTiUkM&list=PLwpjN-4DtVRZfN1GgXCkCNVC9V711zKfg&index=4
    // 11:41
    netlifyIdentity.on('init', async (user) => {
      if (user) {
        this.isLoggedIn = true
      }
    })
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
