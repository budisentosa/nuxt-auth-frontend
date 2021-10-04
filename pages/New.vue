<template>
  <div class="w-4/5 mx-auto md:w-1/2 text-center my-12 overflow-hidden">
    <form ref="form" @submit="createPost">
      <h2 class="font-bold text-2xl md:text-4xl mt-5">Create a new Group</h2>
      <div>
        <input
          v-model="form.Title"
          name="groupName"
          type="text"
          placeholder="Group Name"
          class="p-3 my-3 border w-full"
        />
      </div>
      <div>
        <input
          v-model="form.description"
          name="groupDescription"
          type="text"
          placeholder="group description"
          class="p-3 my-3 border w-full"
        />
      </div>
      <div>
        <button
          class="text-center w-44 px-3 py-2 border rounded border-gray-600 text-gray-600 text-medium hover:bg-gray-900 hover:text-white"
          :disabled="
            form.groupName === '' ||
            form.groupDescription === ''
          "
          type="submit"
        >
          Create
        </button>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        groupName: '',
        groupDescription: '',
        users_permissions_user: this.$strapi.user,
      },
    }
  },
  methods: {
    async createPost(e) {
      const formData = new FormData()
      // let file
      // const formElements = this.$refs.form.elements
      // formElements.forEach((el, i) => {
      //   if (el.type === 'file') {
      //     file = el.files[0]
      //   }
      // })
      // formData.append(`files.image`, file, file.name)
      formData.append('data', JSON.stringify(this.form))
      e.preventDefault()
      await this.$strapi.$groups.create(formData)
      this.$nuxt.$router.push('/groups')
    },
    // assignFileInput() {
    //   const formElements = this.$refs.form.elements
    //   formElements.forEach((el, i) => {
    //     if (el.type === 'file') {
    //       this.fileInput = el.files[0] !== undefined ? el.files[0].name : ''
    //     }
    //   })
    // },
  },
  middleware({ $strapi, redirect }) {
    if (!$strapi.user) {
      redirect('/groups')
    }
  },
}
</script>
<style></style>
