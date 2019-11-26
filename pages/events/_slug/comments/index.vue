<template>
  <div>
    <h5>Event's comments: {{ slug }}</h5>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'Event comment: #' + this.slug
    }
  },
  computed: {
    slug() {
      return this.$route.params.slug + ' Comments'
    }
  }
}
</script>

<style lang="scss" scoped></style>
