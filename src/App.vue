<template>
  <div class="app">
    <ActiveTestAccess/>
  </div>
</template>

<script>
  import ActiveTestAccess from './modules/ActiveTestAccess/index.vue'

  export default {
    components: {
      ActiveTestAccess,
    },
    data() {
      return {
        dd: '4'
      }
    },
  }
</script>

<style lang="sass" scoped>
</style>