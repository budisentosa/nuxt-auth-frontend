<template>
  <div class="min-h-screen bg-gray-300 pb-20">
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
        class="mx-3 p-3 flex flex-col gap-2 bg-white rounded-md shadow-lg "
      >
        <div class=" sm:pr-2 sm:text-left w-full flex flex-col gap-3 items-end">
          <div class="flex justify-between w-full">
            <h3 class="font-bold flex">{{ group.groupName }}</h3>

            <div class="flex gap-2 text-gray-200 items-center px-3 py-1 rounded-full bg-gray-800">
              <p>SRL Level:</p>
              <p class=" text-gray-200 font-semibold">{{ group.srl.level }}</p>
            </div>

          </div>
        </div>
        <div class="flex font-semibold items-center gap-3 text-sm">
          <p>Business Type :</p>
          <h3 class="font-semibold text-gray-600 text-sm">{{ group.type.name }}</h3>
        </div>
        <div class="h-px w-full bg-gray-300"></div>
          <!-- group students -->
          <div class="flex flex-col text-sm font-semibold gap-1 justify-between items-start w-full">
            <h4>Anggota:</h4>
            <div class="flex justify-start gap-6">
                <div v-for="(groupstudent, i2) in group.students" :key="i2">
                    <h3>
                    {{groupstudent.studentName}}
                    </h3>
                    <p class="text-sm">
                       NIM: {{groupstudent.studentNim}}
                    </p>
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
