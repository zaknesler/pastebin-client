<template>
  <div>
    <PasteItem
      v-for="paste in pastes"
      :key="paste.id"
      :paste="paste"
    />
  </div>
</template>

<script>
  import PasteItem from '~/components/pastes/PasteItem'

  export default {
    components: {
      PasteItem
    },

    data () {
      return {
        pastes: []
      }
    },

    created () {
      this.getPastes()
    },

    methods: {
      async getPastes () {
        let { data } = await this.$axios.$get('/pastes')

        this.pastes = data
      }
    }
  }
</script>
