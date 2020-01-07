<template>
  <ul>
    <template v-if="!fetchError">
      <Repo v-for="repo in repos" :key="repo.id" :repo="repo" />
      <RepoPlaceholders v-if="loading" />
    </template>
    <div v-else class="error">{{ fetchError }}</div>
  </ul>
</template>

<script>
import Repo from '../components/Repo'
import RepoPlaceholders from '../components/RepoPlaceholders'
export default {
  name: 'home',
  components: { Repo, RepoPlaceholders },
  data() {
    return {
      repos: [],
      loading: false,
      fetchError: null,
    }
  },
  methods: {
    async fetchPopularGihutbReops() {
      this.loading = true
      const lastMonthDateInms = Date.now() - 1000 * 60 * 60 * 24 * 30
      const lastMonthDate = new Date(lastMonthDateInms).toISOString().slice(0, 10)

      const blob = await fetch(
        `https://api.github.com/search/repositories?q=created:>${lastMonthDate}&sort=stars&order=desc`
      )
      const response = await blob.json()

      if (blob.ok) {
        this.loading = false
        this.repos = response.items
      } else {
        this.fetchError = 'an error occured. Please try later!'
      }
    },
  },
  mounted() {
    this.fetchPopularGihutbReops()
  },
}
</script>

<style scoped>
.error {
  font-size: 2rem;
  color: #e91e63;
}
</style>
