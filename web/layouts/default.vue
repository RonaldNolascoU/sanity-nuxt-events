<template lang="pug">
div
  Navbar(
    :title='$store.state.eventInformation.name',
    :ticket-link='$store.state.eventInformation.ticket'
  )
  .row.m-0
    Sidebar
    nuxt.layout
  Footer
</template>

<script>
import Navbar from '~/components/Navbar.vue'
import Footer from '~/components/Footer.vue'
import Sidebar from '../components/Sidebar.vue'

export default {
  components: {
    Navbar,
    Footer,
    Sidebar
  },
  async mounted() {
    await this.$fire.authReady
    // Timeout before firebase fetches current user
    setTimeout(async () => {
      const user = await this.$fire.auth.currentUser
      console.log(user, 'auth user')
      if (user) {
        this.$store.commit('auth/isAuth', true)
      } else {
        this.$store.commit('auth/isAuth', false)
      }
    }, 600)
  }
}
</script>

<style lang="scss">
// @import '../styles/custom-media.css';
// @import '../styles/custom-properties.css';
@import '../styles/app';

html {
  font-family: var(--font-family-sans);
  font-size: var(--font-base-size);
  line-height: var(--font-base-line-height);
}

.layout {
  flex: 1;
}

body {
  -webkit-font-smoothing: antialiased;
  background: var(--color-white);
  color: var(--color-black);
  margin: 0;
}

html,
body,
#__nuxt,
#__layout,
#__layout > div {
  height: 100%;
}

.title {
  font-weight: 600;
  font-size: var(--font-title2-size);
  line-height: var(--font-title2-line-height);
  margin-bottom: 0.25rem;
  padding-bottom: 0;

  @nest & strong {
    background: #fe0;
  }

  @media (--media-min-medium) {
    font-size: var(--font-title1-size);
    line-height: var(--font-title1-line-height);
  }
}

.title + p {
  font-size: var(--font-large-size);
  line-height: var(--font-large-line-height);
  margin-top: 0;
  margin-bottom: 4rem;

  @media (--media-min-medium) {
    font-size: var(--font-title3-size);
    line-height: var(--font-title3-line-height);
  }
}
</style>
