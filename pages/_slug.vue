<template>
  <div>
    <div class="text-center">
      <div class="text-lg text-grey-darkest font-semibold">
        {{ paste.name }}
      </div>

      <div v-if="paste.user" class="mt-4 text-grey-dark flex items-center justify-center">
        <div class="relative">
          <img :src="paste.user.avatar" class="w-6 h-6 block pointer-events-none rounded-full" alt="Avatar">
          <div class="block absolute pin-x pin-y shadow-inner-hard rounded-full" />
        </div>

        <div class="ml-2">{{ paste.user.username }}</div>
      </div>
    </div>

    <pre v-highlightjs="paste.body" class="mt-8 w-full rounded-lg bg-grey-lightest border border-grey-lighter"><code :class="paste.language" /></pre>
  </div>
</template>

<script>
  import Vue from 'vue'
  import Highlight from 'vue-highlightjs'

  import '~/assets/less/hljs.less'

  Vue.use(Highlight)

  export default {
    data () {
      return {
        paste: null
      }
    },

    async asyncData ({ params, app }) {
      let { data } = await app.$axios.$get(`/pastes/${params.slug}`)

      return {
        paste: data
      }
    }
  }
</script>
