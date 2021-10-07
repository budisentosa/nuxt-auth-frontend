<template>
  <div>
    <Nav/>
    <div class="w-4/5 mx-auto md:w-1/2 my-12 overflow-hidden">
      <h2 class="font-bold text-center text-2xl md:text-4xl mt-5">Create a new Student</h2>
        <form class="mt-8" ref="form" @submit="createPost">
          <label class="block">
            <span class="text-gray-700">Nama Mahasiswa</span>
            <input
            type="text"
            name="studentName"
            placeholder="Nama Mahasiswa"
            class=" mt-1 block p-3 my-3 border w-full"
            >
          </label>

          <label class="block">
            <span class="text-gray-700">Nomor Induk Mahasiswa</span>
            <input
            type="text"
            name="studentNim"
            placeholder="NIM"
            class=" mt-1 block p-3 my-3 border w-full"
            >
          </label>

          <div>
              <sui-dropdown
              multiple
              fluid
              :options="states"
              placeholder='SRL'
              search
              selection
              v-model="current"
              />
          </div>
        </form>
    </div>


  </div>
</template>

<script>
  export default {

    data() {
      return {
        current: null,
        states: [
          {key:'AL', value:'AL', text:'satu'},
          {key:'NC', value:'NC', text:'dua'},
          {key:'RI', value:'RI', text:'tiga'},
          {key:'OH', value:'OH', text:'empat'},
        ],
      }
    }
  }
</script>
