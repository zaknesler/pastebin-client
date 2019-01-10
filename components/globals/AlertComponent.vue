<template>
  <div
    v-if="alert"
    class="p-6 mb-8 rounded-lg w-full bg-green-lightest text-green-darker"
    @click.prevent="clear"
  >
    {{ alert }}
  </div>
</template>

<script>
  import { mapGetters, mapActions } from 'vuex'

  export default {
    computed: {
      ...mapGetters({
        alert: 'alert/message'
      })
    },

    methods: {
      ...mapActions({
        clear: 'alert/clear'
      })
    }
  }
</script>
