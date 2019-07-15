<template>
  <div class="index">
    <div class="container">
      <BlogSection :blogs="blogs"/>
    </div>
  </div>
</template>

<script>
  import BlogSection from "~/components/Sections/BlogSection"

  import blogs from '~/blogs.js'

  export default {
    async asyncData ({app}) {

      async function asyncImport (blogName) {
        const wholeMD = await import(`~/blog/${blogName}.md`)
        return wholeMD.attributes
      }

      return Promise.all(blogs.map(blog => asyncImport(blog)))
      .then((res) => {
        return {
          blogs: res
        }
      })
    },

    components: { BlogSection },

    transition: {
      name: 'slide-fade'
    },

    head () {
      return {
        title: '',
        meta: [
          { name: "author", content: "Anthony Coffey" },
          { name: "description", property: "og:description", content: '', hid: "description" },
          { property: "og:title", content: '' },
          { property: "og:image", content: this.ogImage },
          { name: "twitter:description", content: '' },
          { name: "twitter:image", content: this.ogImage }
        ]
      };
    },

    computed: {
      ogImage: function () {
        return;
      }
    }
  }
</script>
