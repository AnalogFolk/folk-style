<template lang="pug">
  div
    navbar
    nuxt
    af-footer
</template>

<script>
import Navbar from '~/components/global/Header.vue'
import AfFooter from '~/components/global/AfFooter.vue'

export default {
  components: {
    Navbar,
    AfFooter,
  },
  head() {
    return {
      meta: [
        {
          hid: 'og:title',
          property: 'og:title',
          content: this.$i18n.t('homepage.meta.title'),
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.$i18n.t('homepage.meta.description'),
        },
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: this.$i18n.t('homepage.meta.title'),
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: this.$i18n.t('homepage.meta.description'),
        },
      ],
    }
  },
  computed: {
    visible() {
      return true
    },
  },
  watch: {
    // $route: 'setStore'
  },
}
</script>

<style lang="scss">
@import '~assets/sass/base';
html {
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  font-size: 18px;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

body {
  background-color: $off-white;
  color: #000000;
}

p {
  padding-bottom: 1em;
}

.content a {
  color: inherit;
  text-decoration: none;
  position: relative;
  z-index: 0;
  display: inline-block;

  &:hover {
    &:after {
      top: 0%;
    }
  }

  &:after {
    content: '';
    z-index: -1;
    top: 70%;
    left: -0.2em;
    right: -0.2em;
    bottom: 0;
    position: absolute;
    transition: top 200ms cubic-bezier(0, 0.8, 0.13, 1);
    background-color: rgba($brand-red, 0.3);
    border-radius: 5px;
  }
}

ul,
ol {
  li {
    list-style-type: disc;
    p {
      padding-bottom: 0;
    }
  }
  padding-bottom: 1.2em;
}

pre {
  margin-bottom: 1em;
}

.container article {
  @apply pb-0.5 mb-16;
}
</style>
