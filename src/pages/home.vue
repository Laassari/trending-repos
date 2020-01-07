<template>
  <ul>
    <Repo v-for="repo in repos" :key="repo.id" :repo="repo" />
    <RepoPlaceholders v-if="loading" />
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
    }
  },
  methods: {
    async fetchPopularGihutbReops() {
      this.loading = true
      const blob = await fetch('https://api.github.com/search/repositories?q=created:>2017-10-22&sort=stars&order=desc')
      const response = await blob.json()

      this.loading = false
      this.repos = response.items
    },
  },
  mounted() {
    this.fetchPopularGihutbReops()
  },
}
</script>

<style></style>
