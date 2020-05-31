<template>
  <nav class="menu">
    <router-link exact :to="{ name:'home' }">Home</router-link>
    <router-link exact :to="{ name:'faq' }">FAQ</router-link>
    <div class="spacer" v-if="$state.user">
      <a>{{ $state.user.username }}</a>
      <a @click="logout">Logout</a>
    </div>
    <router-link v-else :to="{ name: 'login' }">Login</router-link>
    <router-link :to="{ name: 'tickets' }">Support tiekets</router-link>
  </nav>
</template>

<script>
export default {
  methods: {
    async logout () {
      const result = await this.$fetch('logout')
      if (result.status === 'ok') {
        this.$state.user = null
        this.$router.push({name: 'home'})
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../style/imports';

.router-link-active {
  border-bottom-color: $primary-color;
}
</style>