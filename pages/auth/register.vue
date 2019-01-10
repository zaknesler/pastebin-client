<template>
  <form class="mt-24 max-w-sm mx-auto" @submit.prevent="login">
    <h3 class="text-xl text-center font-semibold text-grey-darkest mb-8">Sign up</h3>

    <div class="w-full mb-4">
      <div class="w-full">
        <label class="inline-block text-grey-dark text-sm mb-2" for="username">Username</label>

        <input
          id="username"
          v-model="form.username"
          tabindex="1"
          class="w-full h-full appearance-none text-base text-grey-darker border-0 bg-grey-lightest focus:outline-none focus:shadow-outline shadow-transition p-4 rounded-lg"
          placeholder="Username"
          type="text"
          autofocus
          required
        >
      </div>
    </div>

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
        username: '',
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
        await this.$axios.$post('/auth/register', {
          ...this.form
        }).then(({ data }) => {
          this.flash('Your account has been registered and you may now sign in.')

          if (this.$route.query.redirect) {
            this.$router.replace(this.$route.query.redirect)

            return
          }

          this.$router.replace({
            name: 'auth-login'
          })
        })
        .catch(({ response }) => {
          this.flash('We could not register your account.')
        })
      }
    }
  }
</script>
