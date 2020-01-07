<template>
  <div id="infinite_scroll">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'infiniteScroll',
  props: {
    // distance from the bottom where we should emit events in pixels
    treshhold: {
      default: 400,
      type: Number,
    },
  },
  methods: {
    handleScroll() {
      const wrapper = document.getElementById('infinite_scroll')

      // bottom of wrapper
      const wrapperOffset = wrapper.offsetTop + wrapper.offsetHeight

      const bottomOfPage = (window.scrollY || window.pageYOffset) + window.innerHeight
      const reachedBottom = bottomOfPage > wrapperOffset - this.treshhold
      if (reachedBottom) {
        this.$emit('bottom-reached')
      }
    },
  },

  mounted() {
    // TODO: add throttling
    addEventListener('scroll', this.handleScroll)
  },
}
</script>

<style></style>
