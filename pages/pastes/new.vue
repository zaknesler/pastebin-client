<template>
  <div>
    <h3 class="text-xl text-center font-semibold text-grey-darkest mb-8">Create Paste</h3>

    <div class="w-full mb-4">
      <div class="w-full">
        <label class="inline-block text-grey text-sm font-semibold mb-2" for="name">Name</label>

        <input
          id="name"
          v-model="form.name"
          tabindex="1"
          class="w-full h-auto appearance-none text-base text-grey-darker border-0 bg-grey-lightest focus:outline-none focus:shadow-outline shadow-transition p-4 rounded-lg"
          placeholder="Name"
          type="text"
          autofocus
        >
      </div>
    </div>

    <div class="w-full flex flex-col sm:flex-row">
      <div class="w-full sm:w-1/3 mb-4 sm:mr-2">
        <label class="inline-block text-grey text-sm font-semibold mb-2" for="visibility">Visibility</label>

        <Dropdown
          id="visibility"
          v-model="form.visibility"
          :items="visibilities"
          tabindex="2"
        />
      </div>

      <div class="w-full sm:w-1/3 mb-4 sm:mx-2">
        <label class="inline-block text-grey text-sm font-semibold mb-2" for="language">Language</label>

        <Dropdown
          id="language"
          v-model="form.language"
          :items="languages"
          tabindex="3"
        />
      </div>

      <div class="w-full sm:w-1/3 mb-4 sm:ml-2">
        <label class="inline-block text-grey text-sm font-semibold mb-2" for="expires_at">Expiration</label>

        <Dropdown
          id="expires_at"
          v-model="form.expires_at"
          :items="expirations"
          tabindex="4"
        />
      </div>
    </div>

    <div class="w-full mb-4">
      <label class="inline-block text-grey text-sm font-semibold mb-2" for="body">Body</label>

      <textarea
        id="body"
        v-model="form.body"
        rows="20"
        class="w-full h-full whitespace-no-wrap overflow-auto resize-y leading-normal font-mono appearance-none text-sm text-grey-darker border-0 bg-grey-lightest focus:outline-none focus:shadow-outline shadow-transition p-4 rounded-lg"
        tabindex="5"
      />
    </div>

    <div class="text-right">
      <input
        class="inline-block px-6 py-3 rounded-lg cursor-pointer appearance-none w-auto h-auto text-base text-white bg-green hover:bg-green-dark focus:outline-none focus:shadow-outline shadow-transition"
        type="submit"
        value="Create"
        tabindex="6"
        @click.prevent="submit"
      >
    </div>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'

  import Dropdown from '~/components/pastes/Dropdown'

  export default {
    components: {
      Dropdown
    },

    data: () => ({
      form: {
        name: '',
        language: '',
        visibility: '',
        expires_at: '',
        body: '',
      }
    }),

    computed: {
      ...mapGetters({
        visibilities: 'dropdowns/visibilities',
        languages: 'dropdowns/languages',
        expirations: 'dropdowns/expirations'
      })
    },

    methods: {
      submit () {
        this.$axios.$post('/pastes', this.form)
          .then(({ data }) => {
            if (data.error) {
              return
            }

            this.$router.push({ name: 'slug', params: { slug: data.slug } })
          })
      }
    }
  }
</script>
