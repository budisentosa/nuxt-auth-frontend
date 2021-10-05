<template>
  <div class="min-h-screen flex justify-center items-center text-center relative mx-auto">
    <img class="absolute inset-y-0 inset-x-auto object-cover w-full h-full opacity-50" src="../assets/img/97363.jpeg" alt="">
    <div class="absolute inset-auto w-3/4  md:left-8 md:w-1/2">
      <h1 class="py-4 px-2 border-2 border-gray-600 my-12 text-3xl md:text-6xl text-center leading-relaxed text-gray-600 font-light tracking-wide ">Student Assessment Management System</h1>
      <div class="flex flex-col gap-12 md:flex-row mx-auto items-center justify-center">
        <NuxtLink to="/login" class="text-center w-44 px-3 py-2 border rounded border-gray-700 text-gray-600 text-medium hover:bg-gray-700 hover:text-white"> Login </NuxtLink>
        <NuxtLink to="/groups" class="text-center w-44 px-3 py-2 border rounded border-gray-700 text-gray-600 text-medium hover:translate-y-3 hover:bg-gray-700 hover:text-white"> Continue </NuxtLink>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  middleware: 'authenticated',
}
</script>
<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
/* .container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 80px;
  color: #35495e;
  letter-spacing: 1px;
}
.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links {
  padding-top: 15px;
} */
</style>
