<template>
  <section>
    <div class="blogs__top">
      <div>
        <h2></h2>
        <span class="emoji-title emoji--writing"/>
      </div>
    </div>
    <ul class="blogs">
      <blog-card
        v-for="blog in blogs"
        :key="blog.name"
        :blog="blog" />
    </ul>
  </section>
</template>
<script>
import BlogCard from "~/components/BlogCard.vue";

export default {
  components: { BlogCard },
  props: {
    blogs: {
      type: Array
    }
  }
}
</script>
<style lang="scss">
</style>

