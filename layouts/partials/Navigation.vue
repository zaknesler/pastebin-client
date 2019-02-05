<template>
  <nav class="mb-8 max-w-md mx-auto flex items-baseline justify-between">
    <div class="-mr-6 flex items-baseline">
      <nuxt-link
        :to="{ name: 'pastes' }"
        :class="onPage('pastes') ? 'text-black' : 'text-grey-dark hover:text-grey-darker'"
        class="mr-6 uppercase tracking-wide font-semibold text-xs no-underline"
      >
        Pastes
      </nuxt-link>

      <nuxt-link
        :to="{ name: 'pastes-new' }"
        class="mr-6 px-2 py-1 rounded bg-green-lightest hover:bg-green-lighter text-green-dark uppercase tracking-wide font-semibold text-xs no-underline"
      >
        New Paste
      </nuxt-link>
    </div>

    <div v-if="$auth.loggedIn" class="-mr-6 flex items-baseline">
      <nuxt-link
        :to="{ name: 'my-pastes' }"
        :class="onPage('my-pastes') ? 'text-black' : 'text-grey-dark hover:text-grey-darker'"
        class="mr-6 uppercase tracking-wide font-semibold text-xs no-underline"
      >
        My Pastes
      </nuxt-link>

      <a
        class="mr-6 text-grey-dark hover:text-grey-darker cursor-pointer uppercase tracking-wide font-semibold text-xs no-underline"
        @click.prevent="$auth.logout()"
      >
        Logout
      </a>
    </div>

    <div v-else class="-mr-6 flex items-baseline">
      <nuxt-link
        :to="{ name: 'auth-login' }"
        :class="onPage('auth-login') ? 'text-black' : 'text-grey-dark hover:text-grey-darker'"
        class="mr-6 uppercase tracking-wide font-semibold text-xs no-underline"
      >
        Sign in
      </nuxt-link>

      <nuxt-link
        :to="{ name: 'auth-register' }"
        :class="onPage('auth-register') ? 'text-black' : 'text-grey-dark hover:text-grey-darker'"
        class="mr-6 uppercase tracking-wide font-semibold text-xs no-underline"
      >
        Register
      </nuxt-link>
    </div>
  </nav>
</template>

<script>
  export default {
    methods: {
      onPage (name) {
        return $nuxt.$route.name == name
      }
    }
  }
</script>
