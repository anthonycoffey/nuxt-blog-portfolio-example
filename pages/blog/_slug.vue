<template>
  <div>
    <span class="date">{{ date }}</span>

    <header>
      <h1>
        {{ title }}
      </h1>
    </header>

    <DynamicMarkdown
      :render-func="renderFunc"
      :static-render-funcs="staticRenderFuncs"/>

    <nuxt-link class="badge badge--big" to="/">
      Go Back
    </nuxt-link>
  </div>
</template>

<script lang="js">

  import DynamicMarkdown from "~/components/Markdown/DynamicMarkdown.vue"


  export default {

    async asyncData ({params, app}) {
      const fileContent = await import(`~/blog/${params.slug}.md`)
      const attr = fileContent.attributes
      return {
        name: params.slug,
        title: attr.title,
        // trans: attr.trans,
        date: attr.date,
        // id: attr.id,
        // owner: attr.owner,
        // colors: attr.colors,
        // role: attr.role,
        // cardAlt: attr.cardAlt,
        // noMainImage: attr.noMainImage,
        description: '',
        // related: attr.related,
        // extraComponent: attr.extraComponent,
        renderFunc: fileContent.vue.render,
        staticRenderFuncs: fileContent.vue.staticRenderFns,
        image: {
          // main: attr.image && attr.image.main,
          // og: attr.image && attr.image.og
        }
      }
    },

    components: { DynamicMarkdown},

    head () {
      return {
        title: this.pageTitle,
        meta: [
          { name: "author", content: "Anthony Coffey" },
          { name: "description", property: "og:description", content: this.description, hid: "description" },
          { property: "og:title", content: this.pageTitle },
          { property: "og:image", content: this.ogImage },
          { name: "twitter:description", content: this.description },
          { name: "twitter:image", content: this.ogImage }
        ],
      };
    },

    transition: {
      name: 'slide-fade'
    },

    computed: {
      ogImage () {
        return ''
        // return `/images/${this.id}`;
      },
      pageTitle () {
        return this.title
      },

    }
  }
</script>

<style lang="scss">

</style>
