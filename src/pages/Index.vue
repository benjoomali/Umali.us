<template>
  <Layout class="bg-white">
    <main>
      <header class="bg-blue-500 bg-cover bg-center opacity-75" style="background-image:url('/images/hero-image-umali-us-1.jpg')">
        
        <div class="max-w-xl md:max-w-3xl xl:max-w-4xl mx-auto text-center px-6 py-10 md:py-32">
          <h1 class="text-4xl sm:text-5xl md:text-6xl font-sans font-extrabold mt-5">
            <g-link to="/" class="text-red-700">The Umalis</g-link>
          </h1>


        </div>
      </header>
      <div class="max-w-xl md:max-w-3xl xl:max-w-4xl mx-auto text-center px-6 py-4 md:py-12">
        <h2 class="text-gray-800 text-lg sm:text-3xl font-sans font-bold text-center">Pictures from the Wedding, Honeymoon and More!</h2>
        <h2 class="text-gray-700 text-md sm:text-2xl font-sans text-center">Thank you always for your support and love.</h2>
        </div>
        <section>
            <article>
            <div class="mx-auto max-w-3xl bg-indigo-100 px-6">
              <div class="py-8 sm:py-10 border-b border-gray-300">
                <header class="text-center mb-8">
                  <div class="text-gray-700 text-xs mb-2 uppercase">12 October, 2019</div>
                  <h2 class="text-3xl sm:text-4xl leading-tight font-sans mb-1 sm:mb-2">
                    <span class="text-black font-bold"><a target="_blank" href="https://three16photography.client-gallery.com/gallery/umali-wedding-or-october-12th-2019">The Wedding</a></span>
                  </h2>
                </header>
                <p class="leading-normal text-gray-700 text-lg px-2 sm:px-4 md:px-10"><strong>Three16 Photography</strong> did a fantastic job shooting our wedding! If you'd like to see some of the pictures, you can visit their website.</p>
                <p class="leading-normal font-bold text-gray-800 text-lg md:text-center px-2 py-2 sm:px-4 md:px-10 mb-5"><a class="underline font-bold" target="_blank" href="https://three16photography.client-gallery.com/gallery/umali-wedding-or-october-12th-2019">You can view the photos here.</a></p>
                <div class="mx-auto flex items-center justify-center mb-3"> 
                  <iframe src="https://player.vimeo.com/video/386891861" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

                  </div>
                  <p class="self-center text-center tracking-tight font-semibold text-gray-800"><a href="https://vimeo.com/386891861">Ben + Danielle | Wedding Highlight Film</a> from <a href="https://vimeo.com/three16photography">Jerrick O&#039;Connor</a>.</p>
              </div>
            </div>
          </article>
        </section>
      <section>
        <post-item v-for="edge in $page.posts.edges" :key="edge.node.id" :post="edge.node" />
      </section>
      <pagination :info="$page.posts.pageInfo" v-if="$page.posts.pageInfo.totalPages > 1" />
      <site-footer class="py-8 sm:py-16" />
    </main>
  </Layout>
</template>

<script>
import config from '~/.temp/config.js'
import SiteFooter from '@/components/Footer'
import PostItem from '@/components/PostItem'
import Pagination from '@/components/Pagination'

export default {
  components: {
    PostItem,
    Pagination,
    SiteFooter,
  },
  metaInfo () {
    return {
      title: this.$static.metadata.siteName,
      meta: [
        { property: "og:type", content: 'website' },
        { property: "og:title", content: this.$static.metadata.siteName },
        { property: "og:description", content: this.$static.metadata.siteDescription },
        { property: "og:url", content: this.$static.metadata.siteUrl },
        { property: "og:image", content: this.ogImageUrl },

        { name: "twitter:card", content: "summary_large_image" },
        { name: "twitter:title", content: this.$static.metadata.siteName },
        { name: "twitter:description", content: this.$static.metadata.siteDescription },
        { name: "twitter:site", content: "@cossssmin" },
        { name: "twitter:creator", content: "@cossssmin" },
        { name: "twitter:image", content: this.ogImageUrl },
      ],
    }
  },
  computed: {
    config () {
      return config
    },
    ogImageUrl () {
      return `${this.config.siteUrl}/hero-image-umali-us-1.jpg`
    }
  },
}
</script>

<page-query>
  query Home ($page: Int) {
    posts: allPost (page: $page, perPage: 6) @paginate {
      totalCount
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          id
          title
          timeToRead
          datetime: date (format: "YYYY-MM-DD HH:mm:ss")
          content
          excerpt
          description
          path
          cover
          tags {
            id
            title
            path
          }
          author {
            id
            title
            path
          }
        }
      }
    }
  }
</page-query>

<static-query>
query {
  metadata {
    siteName
    siteUrl
    siteDescription
  }
}
</static-query>
