<template>
  <div class="page-index">
<!--    <div class="section" style="transform-origin: center top; transform: scaleY(1);">-->
<!--      <div class="image-parallax" style="position: sticky; top: 0; width: 100vw; z-index: -2;">-->
<!--        <img src="~assets/images/par.jpeg" style="width: 100%;" />-->

<!--      </div>-->
<!--      <div class="content-parallax" style="position: relative; margin: -50vh auto 0; color: white; height: 500px;">-->
<!--        <h1>Zwycięscy i przegrani mają te same cele</h1>-->
<!--      </div>-->
<!--    </div>-->

    <div class="main" style="">
      <div>
        <div style="text-align: center;">
          <h1>Hello</h1>
        </div>
      </div>
      <div>

      </div>
    </div>
    <div class="container">
<!--      <div class="logo" style="display: grid; grid-template-columns: 30% auto 30%; margin-top: 50px;">-->
<!--        <div style="grid-column-start: 2; margin-bottom: 50px;">-->
<!--          <image-responsive-->
<!--              imageURL="logo1500x1500.png"-->
<!--              alt="performance" />-->
<!--        </div>-->
<!--      </div>-->
      <BlogSection :blogs="blogs"/>
    </div>
  </div>
</template>

<script>
  import BlogSection from "~/components/Sections/BlogSection"

  import blogs from '~/contents/blogsEn.js'

  export default {
    async asyncData () {

      async function asyncImport (blogName) {
        const wholeMD = await import(`~/contents/blog/${blogName}.md`)
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
        title: this.title,
        htmlAttrs: {
          lang: "pl",
        },
        script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }],
        meta: [
          { name: "author", content: "Stanisław Stępak" },
          { name: "description", property: "og:description", content: "TODO: Dodać meta-description", hid: "description" },
          { property: "og:title", content: this.title },
          { property: "og:image", content: this.ogImage },
          { name: "twitter:description", content: this.title },
          { name: "twitter:image", content: this.ogImage }
        ]
      };
    },

    computed: {
      title() {
        return "Planer Osobisty"
      },
      ogImage: function () {
        return;
      },
      bgImageUrl() {
        return require('~/assets/images/par.jpeg');
      }
    }
  }
</script>

<style>
.main {
  background-image: url('~assets/images/par.jpeg');
  width: 100%;
  min-height: 100vh;
  background-size: cover;
  padding-top: 30vh;
}
.main h1 {
  color: white;
  font-size: 100px;
}
</style>