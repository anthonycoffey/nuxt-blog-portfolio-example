<template>
  <li class="blog">
    <nuxt-link
      :to="{ name: 'blog-slug', params: { slug: slug }}"
    >
      <h3 class="blog__title">
        {{ blog.title }}
      </h3>
      <p class="blog__description">
        {{ blog.description }}
      </p>
    </nuxt-link>
  </li>
</template>

<script lang="js">
  export default {
    props: {
      blog: {
        type: Object
      }
    },
    data(){
      return {
        slug: ''
      }
    },
    created() {
      const path = this.blog._meta.resourcePath;
      const str = path.split('/blog/')[1]
      this.slug = str.replace('.md','');
    }
  }
</script>

<style lang="scss">

</style>
