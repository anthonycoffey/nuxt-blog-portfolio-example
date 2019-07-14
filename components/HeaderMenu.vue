<template>
  <div class="row bg-primary">
    <div class="container">
      <nav class="main-menu text-white">
        <ul>
          <li v-for="(link,index) in links" :key="index">
            <nuxt-link v-bind:to="link.route" class="button button--green">{{ link.name }}</nuxt-link>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HeaderMenu',
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
