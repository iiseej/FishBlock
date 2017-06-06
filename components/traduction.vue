<template lang="html">
  <div class="trad">
    <nuxt-link class="Header__Link" v-if="$i18n.locale === 'en'" :to="`/fr` + $route.fullPath" active-class="none" exact>
      <img src="~assets/franceicon.png" :alt="$t('links.french')"/>
    </nuxt-link>
    <nuxt-link class="Header__Link" v-else :to="$route.fullPath.replace(/^\/[^\/]+/, '')" active-class="none" exact>
      <img src="~assets/englishicon.png" :alt="$t('links.english')"/>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  methods: {
    path (url) {
      return (this.$i18n.locale === 'en' ? url : '/' + this.$i18n.locale + url)
    }
  }
}
</script>

<style lang="css">
.Header__Link img {
  padding-top: 11px;
}
</style>
