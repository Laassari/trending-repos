<template>
  <div>
    <RepoPlaceholder v-for="i in count" :key="i" class="placeholder-wrapper" />
  </div>
</template>

<script>
import RepoPlaceholder from './RepoPlaceholder'
export default {
  name: 'RepoPlaceholders',
  components: { RepoPlaceholder },
  props: {
    count: {
      default: 3,
      type: Number,
    },
  },
}
</script>

<style scoped>
.placeholder-wrapper {
  margin-bottom: 1rem;
}
</style>
