<template>
  <div class="container">
    <div>
      <h1 class="my-12 text-5xl text-center leading-relaxed text-gray-500 font-light ">Student Assessment Management System</h1>
      <div class="flex flex-col gap-3 md:flex-row mx-auto items-center justify-center">
        <NuxtLink to="/login" class="text-center w-44 px-3 py-2 border rounded border-gray-600 text-gray-600 text-medium hover:bg-gray-500 hover:text-white"> Login </NuxtLink>
        <NuxtLink to="/groups" class="text-center w-44 px-3 py-2 border rounded border-gray-600 text-gray-600 text-medium hover:translate-y-3 hover:bg-gray-500 hover:text-white"> Continue </NuxtLink>
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
