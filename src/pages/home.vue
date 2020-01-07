<template>
  <ul>
    <template v-if="!fetchError">
      <InfiniteScroll @bottom-reached="bottomReachedHandler">
        <Repo v-for="repo in repos" :key="repo.id" :repo="repo" />
        <RepoPlaceholders v-if="loading" />
      </InfiniteScroll>
    </template>
    <div v-else class="error">{{ fetchError }}</div>
  </ul>
</template>

<script>
import Repo from '../components/Repo'
import RepoPlaceholders from '../components/RepoPlaceholders'
import InfiniteScroll from '../components/InfiniteScroll'

export default {
  name: 'home',
  components: { Repo, RepoPlaceholders, InfiniteScroll },
  data() {
    return {
      repos: [],
      loading: false,
      fetchError: null,
      page: 1,
    }
  },
  methods: {
    async fetchPopularGihutbReops() {
      this.loading = true
      const lastMonthDateInMs = Date.now() - 1000 * 60 * 60 * 24 * 30
      const lastMonthDate = new Date(lastMonthDateInMs).toISOString().slice(0, 10)

      const blob = await fetch(
        `https://api.github.com/search/repositories?q=created:>${lastMonthDate}&sort=stars&order=desc&page=${this.page}`
      )
      const response = await blob.json()
      this.loading = false

      if (blob.ok) {
        this.repos = [...this.repos, ...response.items]
        this.page++
      } else {
        this.fetchError = 'an error occured. Please try later!'
      }
    },

    bottomReachedHandler() {
      if (this.loading) return

      this.fetchPopularGihutbReops()
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
