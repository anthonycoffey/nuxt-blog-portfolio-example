<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-3">
        <img src="/images/anthony-coffey.jpg"/>
      </div>
      <div class="col-sm-9">

        <h1>My name is Anthony Coffey</h1>

        <p>I am a software engineer based in Austin, Texas. I specialize in web application development using JavaScript, but I’m also proficient with dozens of other languages, frameworks, and libraries.</p>

        <h2>My Accomplishments</h2>

        <p>In 2014, I worked on the development team at RiskProAdvisor.com that was responsible for building out the prototype that helped the company raise a 1.9 million dollar development budget in seed funding.</p>

        <p>Since then, I’ve helped hundreds of small to medium sized businesses make an impact on their bottom line and save millions by automating time consuming tasks that have long since been done by hand.</p>

        <p>For more details about my skill set and work experience, view my resume.</p>

        <h2>My Mission</h2>
        <p>What I bring to the table is more than a maker mentality. I solve big problems, and sometimes those solutions don’t involve any code at all. However, they always involve technology, and I’m here to help your business use the latest in cutting-edge technology to it’s advantage!</p>

        <p>I’m very passionate about software development and education. I have a goal to reach 1,000 people in the next year by teaching them how to code on YouTube and how to make money running their own business writing software for the web.</p>

        <h2>Why?</h2>
        <p>Because I love my work! The intersection of business and technology is fascinating to me, and I spend much of my free-time learning about it.</p>

        <p>Thanks for visiting my blog, I hope you find something useful while you’re here! Be sure to check back soon, and don’t forget to follow me on Behance, Twitter , Instagram and Facebook!!</p>

        <p>
          Best Regards,<br>
          Anthony Coffey
        </p>
      </div>
    </div>
  </div>
</template>

<script>


  export default {
    async asyncData ({app}) {

    },

    components: { },

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
