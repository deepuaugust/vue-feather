<template>
  <button class="btn btn-primary" @click.prevent="onClick">
    {{ n }}
  </button>
</template>

<script>

  export default {
    data () {
      return {
        n: 1
      }
    },
    methods: {
      onClick: function(){
        return this.n += 1
      }
    }
  }
</script>

<style lang="scss" scoped>
</style>
