<template>
  <li>
    <a class="avatar-wrapper" :href="repo.owner.avatar_url">
      <img class="avatar" :src="repo.owner.avatar_url" alt="owner's avatar" />
    </a>
    <div class="content">
      <a :href="repo.html_url" class="title">{{ repo.name }}</a>
      <p class="description">{{ repo.description }}</p>
      <div class="stats-wrapper">
        <span class="stats">Stars: {{ repo.watchers }}</span>
        <span class="stats">Issues: {{ repo.open_issues_count }}</span>
        <span
          >Submitted {{ daysSinceCreated }} days ago by
          <a class="link" :href="repo.owner.html_url"> {{ repo.owner.login }}</a></span
        >
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: 'RepoComponent',
  props: {
    repo: {
      required: true,
      type: Object,
    },
  },
  computed: {
    daysSinceCreated() {
      const startDate = new Date(this.repo.created_at)
      const endDate = new Date()
      let days = 0

      while (endDate > startDate) {
        days++
        startDate.setDate(startDate.getDate() + 1)
      }

      return days
    },
  },
}
</script>

<style scoped>
li {
  list-style: none;
  display: flex;
  margin-bottom: 1.5rem;
  box-shadow: 0 0 4px black;
  padding: 0.7rem;
}
.avatar-wrapper {
  width: 100px;
  height: 100px;
  margin-right: 1rem;
}
.avatar {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.title {
  font-size: 1.5rem;
  text-decoration: none;
  color: inherit;
}
.description {
  flex-grow: 1;
}
.content {
  display: flex;
  flex-direction: column;
}
.stats-wrapper {
  display: flex;
  align-items: center;
}
.stats {
  border: 1px solid #ddd;
  padding: 0.3rem;
  margin-right: 0.3rem;
}

.link {
  color: inherit;
}
</style>
