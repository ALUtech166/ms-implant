<template>
  <div>
    <div class="tw-relative tw-w-full tw-h-72">
      <img class="tw-absolute tw-top-0 tw-left-0 tw-w-full tw-h-full tw-object-cover"
        src="https://img.freepik.com/premium-photo/african-american-practitioner-assistant-with-protective-face-mask-against-coroanvirus_482257-26733.jpg?w=740"
        alt="Banner Image">
      <div
        class="tw-relative tw-w-full tw-h-full tw-flex tw-flex-col tw-justify-center tw-text-center tw-items-center tw-bg-gray-900 tw-bg-opacity-60">
        <h1 class="lg:tw-text-4xl tw-text-xl tw-font-bold tw-text-white">{{ post.title }}</h1>
      </div>
    </div>

    <div class="tw-flex tw-items-center tw-space-x-2 tw-px-8">
      <v-breadcrumbs :items="breadcrumbItems" divider="/" class="tw-text-lg tw-font-extrabold"></v-breadcrumbs>
    </div>

    <div class="tw-bg-white">
      <div class="markdown-body">
        <v-container>
          <v-row>
            <v-col cols="12" md="12">
              <v-card-text>
                <!-- Blog Post Content -->
                <img :src=post.feature_image class="tw-w-full tw-rounded-lg tw-shadow-2xl tw-mb-3">



                <h1 class="lg:tw-text-3xl tw-text-2xl tw-pt-4 tw-font-extrabold tw-text-blue-600">{{ post.title }}</h1>
                <v-list-item-subtitle class="tw-mt-2 tw-text-lg tw-font-extrabold tw-text-blue-600">
                  {{ new Date(post.created_at).toLocaleDateString('fr-FR', {year: 'numeric', month: 'short', day: 'numeric'}) }}
                </v-list-item-subtitle>

                <div class="tw-text-justify tw-mb-4" v-html="post.html" />

                <v-card-actions>
                  <nuxt-link to="/blog"
                    class="tw-group tw-relative tw-font-extrabold xl:tw-px-6 tw-px-4 tw-py-2 tw-mb-4 xl:tw-py-3 tw-rounded-lg tw-shadow-2xl tw-h-12 tw-mt-4 tw-cursor-pointer hover:tw-transform hover:tw-translate-x-2 hover:tw-transition-transform hover:tw-duration-300 hover:tw-shadow-blue-600 tw-border hover:tw-shadow-lg tw-overflow-hidden tw-rounded-lg tw-bg-white tw-text-lg tw-shadow-2xl">
                    <div
                      class="tw-absolute tw-inset-0 tw-w-5 tw-bg-blue-600 tw--transition-all tw-duration-[250ms] tw-ease-out group-hover:tw-w-full">
                    </div>
                    <span
                      class="tw-relative tw-inline-flex tw-items-center tw-gap-2 tw-text-black group-hover:tw-text-white">
                      <svg class="tw-w-5 tw-h-5 tw--transition-all tw-duration-[250ms] tw-ease-out" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                        <path
                          d="M20 11H7.414l5.293-5.293a1 1 0 1 0-1.414-1.414l-7 7a.997.997 0 0 0-.001 1.414l7 7a1 1 0 0 0 1.414-1.414L7.414 13H20a1 1 0 0 0 0-2z" />
                      </svg>

                      Retour aux actualités
                    </span>
                  </nuxt-link>
                </v-card-actions>


              </v-card-text>
            </v-col>

          </v-row>
        </v-container>

      </div>
    </div>
  </div>
</template>

<script>
import AOS from 'aos';
import 'aos/dist/aos.css';
  import {
    getSinglePost
  } from '../api/posts';

  export default {
    async asyncData({
      params
    }) {
      const post = await getSinglePost(params.slug);
      return {
        post: post
      }
    },

    head() {
      return {
        title: 'Slug News Page',

      }
    },

    mounted() {
      if (!this.initialized) {
        AOS.init({
          once: true,
          duration: 2000
        });
        this.initialized = true;
      }
    },

    computed: {
      breadcrumbItems() {
        const items = [{
            text: 'Accueil',
            href: '/',
          },
          {
            text: 'Actualités',
            href: '/blog',

          },
          {
            text: 'Slug Actualités',


          },

        ];

        return items.map((item) => ({
          ...item,
          disabled: !item.href,
        }));
      },
    },
  }

</script>
<style>
  .markdown-body {
    box-sizing: border-box;
    min-width: 200px;
    max-width: 980px;
    margin: 0 auto;
    padding: 45px;
  }

  @media (max-width: 767px) {
    .markdown-body {
      padding: 15px;
    }
  }

  .text-color {
    color: #070A52;
    /* Remove focus outline */
  }

</style>
