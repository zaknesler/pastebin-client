<template>
  <form class="mt-24 max-w-sm mx-auto" @submit.prevent="login">
    <h3 class="text-xl text-center font-semibold text-grey-darkest mb-8">Sign in</h3>

    <div class="w-full mb-4">
      <div class="w-full">
        <label class="inline-block text-grey-dark text-sm mb-2" for="email">Email</label>

        <input
          id="email"
          v-model="form.email"
          tabindex="1"
          class="w-full h-full appearance-none text-base text-grey-darker border-0 bg-grey-lightest focus:outline-none focus:shadow-outline shadow-transition p-4 rounded-lg"
          placeholder="Email"
          type="email"
          autofocus
          required
        >
      </div>
    </div>

    <div class="w-full mb-4">
      <div class="w-full">
        <label class="inline-block text-grey-dark text-sm mb-2" for="password">Password</label>

        <input
          id="password"
          v-model="form.password"
          tabindex="1"
          class="w-full h-full appearance-none text-base text-grey-darker border-0 bg-grey-lightest focus:outline-none focus:shadow-outline shadow-transition p-4 rounded-lg"
          placeholder="Password"
          type="password"
          autofocus
          required
        >
      </div>
    </div>

    <div class="text-right">
      <input
        class="inline-block px-8 py-3 rounded-lg cursor-pointer appearance-none w-auto h-auto text-base text-white bg-green hover:bg-green-dark focus:outline-none focus:shadow-outline shadow-transition"
        type="submit"
        value="Sign in"
        tabindex="6"
      >
    </div>
  </form>
</template>

<script>
  import { mapActions } from 'vuex'

  export default {
    data: () => ({
      form: {
        email: '',
        password: '',
      }
    }),

    middleware: [
      'redirectIfAuthenticated'
    ],

    methods: {
      ...mapActions({
        flash: 'alert/flash'
      }),

      async login () {
        await this.$auth.loginWith('local', {
          data: this.form
        })
      }
    }
  }
</script>
