<template>
<div class="relative min-h-screen bg-no-repeat bg-cover bg-top flex justify-center items-center text-center opacity-80 mx-auto" style="background-image: url(https://cdn.pixabay.com/photo/2018/08/27/15/17/fishing-3635221_960_720.png);">
    <div class="w-4/5 md:w-1/2 max-w-lg text-center mx-auto">
      <div v-show="error !== ''" class="p-3 border">
        <p>{{ error }}</p>
      </div>
      <h1 class="font-semibold text-2xl text-white md:text-4xl mt-5">Signup</h1>
      <form @submit="createUser">
        <div>
          <input
            v-model="email"
            class="p-3 my-5 border w-full"
            type="email"
            placeholder="email"
          />
        </div>
        <div>
          <input
            v-model="username"
            class="p-3 my-5 border w-full"
            type="text"
            placeholder="username"
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
            class="mt-12 text-center text-white boder-white w-full px-3 py-2 border rounded text-medium hover:bg-gray-900 hover:text-white"
            :disabled="email === '' || password === '' || username === ''"
            type="submit"
          >
            Signup
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
      email: "",
      username: "",
      password: "",
      error: "",
    };
  },
  methods: {
    async createUser(e) {
      console.log("masuk ke crate uaser");
      e.preventDefault();
      try {
        const newUser = await this.$strapi.register({
          email: this.email,
          username: this.username,
          password: this.password,
        });
        console.log(newUser);
        if (newUser !== null) {
          this.error = "";
          this.$nuxt.$router.push("/groups");
        }
      } catch (error) {
        this.error = error.message;
      }
    },
  },
  middleware: "authenticated",
};
</script>
<style></style>
