<template>
  <div>
    <Nav class="mx-auto sticky top-0" />
    <h1 class="text-center my-5">All our groups</h1>
    <div
      v-show="error !== ''"
      class="sticky z-100 border p-5 m-3 top-0 bg-black text-white text-center mx-auto w-4/5 sm:w-4/5 md:w-4/5 lg:w-1/2"
    >
      <p class="m-1 sm:m-3">{{ error }}</p>
      <button
        class="button--grey"
        @click="resetError()"
      >Ok</button>
    </div>
    <div
      v-for="(group, i) in data"
      :key="i"
      class="sm:flex sm:space-x-5 my-5 rounded-lg shadow-lg mx-auto w-4/5 sm:w-4/5 md:w-4/5 lg:w-1/2"
    >
      <div class="p-3 sm:pr-2 sm:text-left w-full flex flex-col gap-3 items-end">
        <div class="flex justify-between w-full">
          <h3 class="font-bold">{{ group.groupName }}</h3>
          <div>
            <p>Business Type :</p>
            <h3 class="font-semibold text-gray-500">{{ group.type.name }}</h3>
          </div>
          <div>
            <p>SRL Level:</p>
            <h3 class="font-semibold text-gray-500">{{ group.srl.level }}</h3>
            <!-- <h3 class="font-semibold text-gray-500">{{ group.students }}</h3> -->
          </div>
          <div
            v-for="(tmp, i2) in group.students"
            :key="i2"
          >
            <h4>{{ tmp.angkatan }}</h4>

          </div>
        </div>
        <div class="flex justify-between w-full">

          <!-- students ga bisa dipanggil, gua rasa karena 1 group terdiri dari 3 students (kudu v-for?) -->
          <!-- <p>Anggota:</p>
            <h3 class="font-semibold text-gray-500">{{ group.students.angkatan }}</h3> -->
          <button
            class="w-32 border rounded mt-2 px-3 py-1 sm:mb-0"
            @click="readPost(group)"
          >
            Detail
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  async asyncData({ $strapi, $md }) {
    const data = await $strapi.$groups.find();
    return { data };
  },
  data() {
    return {
      error: "",
    };
  },
  methods: {
    readPost(group) {
      if (this.$strapi.user) {
        this.error = "";
        this.$nuxt.$router.push(`/group/${group.id}`);
      } else {
        this.error = "Please Login to read groups";
      }
    },
    resetError() {
      this.error = "";
    },
  },
};
</script>
<style></style>
