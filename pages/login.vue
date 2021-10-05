<template>
  <div class="relative min-h-screen bg-no-repeat bg-cover bg-left flex justify-center items-center text-center opacity-80 mx-auto" style="background-image: url(https://cdn.pixabay.com/photo/2021/08/22/15/39/kid-6565461_1280.jpg);">
    <div class="w-4/5 md:w-1/2 max-w-lg text-center mx-auto">
      <div v-show="error !== ''" class="p-3 border">
        <p class="text-white">{{ error }}</p>
      </div>
      <h1 class="font-semibold text-4xl text-white md:text-4xl mb-5">Login</h1>
      <form @submit="loginUser">
        <div>
          <input
            v-model="identifier"
            class="p-3 my-5 border w-full"
            type="email"
            placeholder="email"
          />
        </div>
        <div>
          <input
            v-model="password"
            class="p-3 my-5 border w-full"
            type="password"
            placeholder="password"
          />
        </div>
        <div>
          <button
            :disabled="identifier === '' || password === ''"
            class="mt-12 text-center text-white boder-white w-full px-3 py-2 border rounded text-medium hover:bg-gray-900 hover:text-white"
            type="submit"
          >
            Login
          </button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      identifier: '',
      password: '',
      error: '',
    }
  },
  methods: {
    async loginUser(e) {
      e.preventDefault()
      try {
        const user = await this.$strapi.login({
          identifier: this.identifier,
          password: this.password,
        })
        console.log(user)
        if (user !== null) {
          this.error = ''
          this.$nuxt.$router.push('/groups')
        }
      } catch (error) {
        this.error = 'Error in login credentials'
      }
    },
  },
  middleware: 'authenticated',
}
</script>
<style></style>
