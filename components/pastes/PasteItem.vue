<template>
  <nuxt-link
    :to="{ name: 'slug', params: { slug: paste.slug } }"
    class="p-6 mb-6 block w-full rounded-lg text-grey-darker hover:text-green-darker bg-grey-lightest hover:bg-green-lightest no-underline font-semibold"
  >
    {{ paste.name }}
  </nuxt-link>
</template>

<script>
  export default {
    props: {
      paste: {
        required: true,
        type: Object
      }
    }
  }
</script>
