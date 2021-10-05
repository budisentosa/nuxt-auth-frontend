<template>

  <div class="w-4/5 mx-auto md:w-1/2 my-12 overflow-hidden">
    <h2 class="font-bold text-center text-2xl md:text-4xl mt-5">Create a new Group</h2>
    <form class="mt-8" ref="form" @submit="createPost">
        <label class="block">
              <span class="text-gray-700">Nama Kelompok</span>
              <input
                v-model="form.groupName"
                name="groupName"
                type="text"
                placeholder="Nama Kelompok"
                class="form-input mt-1 block p-3 my-3 border w-full"
              />
        </label>
        <label class="block mt-8">
            <span class="text-gray-700">Deskripsi Kelompok</span>
            <textarea
              v-model="form.groupDescription"
              name="groupDescription"
              type="text"
              placeholder="Deskripsi Kelompok"
              class="form-textarea mt-1 block p-3 my-3 border w-full"
            />
        </label>
      <div>
        <div class="flex justify-between ">
          <label class="block mt-4 flex-1">
            <span class="text-gray-700">SRL Level</span>
            <select class="form-select mt-1 block border" v-model="form.srl">
              <option
                v-for="(tmp, i) in datasrl2"
                :key=i
                :value="tmp.id"
              >{{ tmp.level }}</option>
            </select>
          </label>

          <label class="block mt-4">
            <span class="text-gray-700">Business Type</span>
              <select class="form-select mt-1 block border w-full" v-model="form.type">
                <option
                  v-for="(tmp, i) in datasrl3"
                  :key="i"
                  :value="tmp.id"
                >{{ tmp.name }}</option>
              </select>
          </label>
        </div>
        <label class="block w-full mt-8">
            <span>Anggota</span>
          <select class=" mt-1 block border w-full"
            v-model="form.students"
            multiple
          >
            <option
              v-for="(tmp, i) in datasrl4"
              :key="i"
              :value="tmp.id"
            >{{ tmp.studentName }}</option>
          </select>
        </label>
      </div>
        <button
          class="text-center w-full mt-10 mx-auto w-44 px-3 py-2 border rounded border-gray-600 text-gray-600 text-medium hover:bg-gray-900 hover:text-white"
          :disabled="
            form.groupName === '' ||
            form.groupDescription === ''
          "
          type="submit"
        >
          Create
        </button>

    </form>
  </div>
</template>
<script>
export default {
  async asyncData({ $strapi, $md }) {
    // const datasrl = await $strapi.find("srls");
    const datasrl2 = await $strapi.$srls.find();
    const datasrl3 = await $strapi.$types.find();
    const datasrl4 = await $strapi.$students.find();
    // console.log(datasrl2);
    return { datasrl2, datasrl3, datasrl4 };
  },
  data() {
    return {
      form: {
        groupName: "",
        groupDescription: "",
        users_permissions_user: this.$strapi.user,
        srl: "",
        type: "",
        students: [],
      },
    };
  },
  methods: {
    async createPost(e) {
      console.log("masuk ke cratepopst");
      const formData = new FormData();
      // let file
      // const formElements = this.$refs.form.elements
      // formElements.forEach((el, i) => {
      //   if (el.type === 'file') {
      //     file = el.files[0]
      //   }
      // })
      // formData.append(`files.image`, file, file.name)
      console.log(JSON.stringify(this.form));
      formData.append("data", JSON.stringify(this.form));
      e.preventDefault();
      console.log(formData);
      await this.$strapi.$groups.create(formData);
      this.$nuxt.$router.push("/groups");
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
      redirect("/groups");
    }
  },
};
</script>
<style></style>
