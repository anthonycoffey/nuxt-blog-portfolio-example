<script lang="js">
  import InlineCode from './InlineCode.vue'
  import hljs from 'highlight.js/lib/highlight'
  import javascript from 'highlight.js/lib/languages/javascript'
  import css from 'highlight.js/lib/languages/css'
  import php from 'highlight.js/lib/languages/php'
  hljs.registerLanguage('javascript', javascript)
  hljs.registerLanguage('css', css)
  hljs.registerLanguage('php', php)

  import 'highlight.js/styles/darcula.css'

  export default {
    props: ["renderFunc", "staticRenderFuncs", "extraComponent"],

    components: {
      InlineCode
    },

    computed: {
      initHighlightJs () {
        let targets = document.querySelectorAll('code')
        targets.forEach((target) => {
          hljs.highlightBlock(target)
        })
      }
    },

    mounted() {
      this.initHighlightJs
    },

    render (createElement) {
      return this.templateRender ? this.templateRender() : createElement("div", "Rendering");
    },

    created () {
      this.templateRender = new Function(this.renderFunc)()
      this.$options.staticRenderFns = new Function(this.staticRenderFuncs)()
    }
  }
</script>
