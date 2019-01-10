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

    <div class="p-4 sm:p-6 mt-6 block w-full rounded-none rounded-lg bg-grey-lightest border border-grey-lighter text-grey-darker text-sm font-mono overflow-x-auto leading-loose whitespace-pre" v-html="paste.body" />
  </div>
</template>

<script>
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
