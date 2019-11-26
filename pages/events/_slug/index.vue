<template>
  <div>
    <h5>Event slug: #{{ slug }}</h5>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'Event slug #' + this.slug
    }
  },
  computed: {
    slug() {
      return this.$route.params.slug
    }
  }
}
</script>

<style lang="scss" scoped></style>
