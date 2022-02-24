<template>
  
  <div v-if="articles" class="container mx-auto my-10 flex flex-col gap-10">
    <nuxt-link to="/">Home</nuxt-link>
    <h1>
      {{articles.data[0].attributes.title}}
    </h1>
    <p>
      {{articles.data[0].attributes.content}}
    </p>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'IndexPage',
  apollo: {
    // Dynamic querying
    articles: {
      query: gql`
        query getArticle($slug: String!) {
          articles(filters: { slug: { eq: $slug } }) {
            data {
              attributes {
                title
                description
                content
                publishedAt
                image {
                  data {
                    attributes {
                      url
                    }
                  }
                }
                author {
                  data {
                    attributes {
                      name
                      picture {
                        data {
                          attributes {
                            url
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      `,
      variables() {
        return {
          // if the route.params.id is null make id = 1
          slug: this.$route.params.slug || 'the-internet-s-own-boy',
        }
      },
    },
  },
}
</script>
