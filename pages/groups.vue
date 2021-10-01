<template>
  <div class="h-screen bg-gray-300">
    <Nav class="mx-auto sticky top-0" />
    <h1 class="text-center font-semibold my-5 uppercase text-2xl">All Groups</h1>
    <div
      v-show="error !== ''"
      class="sticky z-100 border p-5 m-3 top-0 bg-black text-white text-center mx-auto w-4/5 sm:w-4/5 md:w-4/5 lg:w-1/2"
    >
      <p class="m-1 sm:m-3">{{ error }}</p>
      <button class="button--grey" @click="resetError()">Ok</button>
    </div>
    <div class="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
      <div
        v-for="(group, i) in data"
        :key="i"
        class="mx-3 p-3 flex flex-col gap-4 bg-white rounded-md shadow-lg "
      >
        <div class=" sm:pr-2 sm:text-left w-full flex flex-col gap-3 items-end">
          <div class="flex justify-between w-full">
            <h3 class="font-bold flex">{{ group.groupName }}</h3>
            <div>
              <p>Business Type :</p>
              <h3 class="font-semibold text-gray-500 text-sm">{{ group.type.name }}</h3>
            </div>
            <div class="flex gap-2 text-gray-500 font-semibold items-center px-3 py-1 rounded-full  border">
              <p>SRL Level:</p>
              <p class=" text-gray-500 font-semibold">{{ group.srl.level }}</p>
            </div>
          </div>
        </div>
          <!-- group students -->
          <div class="px-3 flex gap-2 justify-between items-start">
            <div v-for="(groupstudent, i2) in group.students" :key="i2">
              <div>
                {{groupstudent.studentName}}
                {{groupstudent.studentNim}}
              </div>
              </div>
          </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  async asyncData({ $strapi, $md }) {
    const data = await $strapi.$groups.find()
    return { data }
  },
  data() {
    return {
      error: '',
    }
  },
  methods: {
    readPost(group) {
      if (this.$strapi.user) {
        this.error = ''
        this.$nuxt.$router.push(`/group/${group.id}`)
      } else {
        this.error = 'Please Login to read groups'
      }
    },
    resetError() {
      this.error = ''
    },
  },
}
</script>
<style></style>
