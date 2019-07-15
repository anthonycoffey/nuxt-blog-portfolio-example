<template>
  <div>
    <header-menu/>
    <div class="container-medium">
      <div class="row">
        <nuxt/>
      </div>
    </div>
  </div>
</template>
<script>
  import HeaderMenu from '../components/HeaderMenu'

  export default {
    components: { HeaderMenu },
    data() {
      return {}
    }
  }
</script>
<style lang="scss">
  .date {
    font-family: $c-font-primary;
  }
</style>
