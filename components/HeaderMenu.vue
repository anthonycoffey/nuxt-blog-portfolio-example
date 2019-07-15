<template>
  <div class="row p-big bg-dark">
    <div class="container">

        <nav class="main-menu text-white">
          <ul>
            <li v-for="(link,index) in links" :key="index">
              <nuxt-link v-bind:to="link.route">
                <NesButton success>{{ link.name }}</NesButton>
              </nuxt-link>
            </li>
          </ul>
        </nav>



    </div>
  </div>
</template>

<script>
  import NesDialog from 'vuenes.css/src/components/NesDialog'
  export default {
    name: 'HeaderMenu',
    components: { NesDialog },
    data(){
      return {
        links: [
          {
            name: 'Home',
            route: '/'
          },
          {
            name: 'Bio',
            route: '/bio'
          },{
            name: 'Portfolio',
            route: '/portfolio'
          },
          {
            name: 'Blog',
            route: '/blog'
          }
        ]
      }
    }
  }
</script>

<style lang="scss">
  nav.main-menu {
    display: flex;
    align-content: center;
    justify-content: center;
    ul {
      margin: 0!important;
      li {
        display: inline-flex;
        margin: modular-scale(1);
        a{
          margin: 0;
        }
      }
    }
  }
</style>
