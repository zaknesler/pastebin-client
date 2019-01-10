<template>
  <div>
    <div class="max-w-lg mx-auto p-8">
      <Navigation />

      <AlertComponent />

      <nuxt/>
    </div>
  </div>
</template>

<script>
  import Navigation from './partials/Navigation'
  import AlertComponent from '~/components/globals/AlertComponent'

  export default {
    components: {
      Navigation,
      AlertComponent
    },

    head: {
      bodyAttrs: {
        class: 'text-base font-sans font-normal leading-normal tracking-normal roman antialiased bg-white text-grey-darker'
      }
    }
  }
</script>
