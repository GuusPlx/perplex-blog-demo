<template>
  <div v-if="articles">
    <div class="container my-10 mx-auto">
      <h1 class="text-4xl text-pink-500">Perplex blog</h1>
      <ul class="grid grid-cols-2 gap-5 ">
        <li v-for="article of articles.data">
          <div class="p-5 shadow-xl rounded-xl">
            <h2>
              {{article.attributes.title}}
            </h2>
            <img class="h-60" :src="article.attributes.image.data.attributes.url" alt="">
            <nuxt-link class="font-bold text-pink-500 my-5" :to="article.attributes.slug">
              View blog post
            </nuxt-link>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'IndexPage',
  apollo: {
    articles: gql`
      query getArticles {
        articles {
          data {
            id
            attributes {
              slug
              title
              category {
                data {
                  attributes {
                    name
                  }
                }
              }
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
  },
}
</script>
