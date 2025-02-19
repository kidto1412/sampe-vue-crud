<script setup lang="ts">
import { onMounted, reactive, ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import DataTable from 'primevue/datatable'
import Column from 'primevue/column'
import ColumnGroup from 'primevue/columngroup' // optional
import Row from 'primevue/row'
import { Button, Dialog } from 'primevue'
import { api } from './plugins/axios'

const modal = ref<boolean>(false)

const handleClick = () => {
  modal.value = true
}

interface IForm {
  nis: string
  name: string
  classRoom: string
  address: string
}

const name = ref<string>('')

const products = ref([])

const onSubmit = async () => {
  try {
    const data = {
      nama: name.value,
    }
    const response = await api.post('/siswa', { ...data })
    if (response.status == 200) {
      alert('success')
    }
  } catch (error) {
    alert(error)
  }
}

const getSiswa = async () => {
  try {
    const response = await api.get('siswa')
    products.value = response.data.data
    console.log(response.data.data)
  } catch (error) {}
}

const selectRow = (data: any) => {
  visible.value = true
  name.value = data.nama
  console.log(data)
}
const deleteUser = async (data: any) => {
  const response = await api.delete(`siswa/${data.id}`)
  getSiswa()
}

const edit = async (id: number) => {
  const response = await api.get(`siswa/${id}`)
}

onMounted(() => {
  getSiswa()
})

const visible = ref<boolean>(false)
</script>

<template>
  <!-- <RouterView />
  <h1>Hello</h1> -->
  <div class="container">
    <!-- <h1 class="flex flex-col mb-6">Hello world !</h1> -->
    <Button label="Show" @click="visible = true" class="m-5" />
    <!-- Dialog -->
    <Dialog v-model:visible="visible" modal header="Edit Profile" :style="{ width: '25rem' }">
      <span class="text-surface-500 dark:text-surface-400 block mb-8"
        >Update your information.</span
      >
      <div class="flex items-center gap-4 mb-4">
        <label for="username" class="font-semibold w-24">Username</label>
        <InputText id="username" class="flex-auto" autocomplete="off" v-model="name" />
      </div>

      <div class="flex justify-end gap-2">
        <Button type="button" label="Cancel" severity="secondary" @click="visible = false"></Button>
        <Button type="button" label="Save" @click="onSubmit()"></Button>
      </div>
    </Dialog>
    <!-- End Dialog -->

    <h5 class="ml-5 mb-3 font-bold">Data Siswa</h5>
    <DataTable :value="products">
      <Column field="nama" header="Nama"></Column>
      <Column field="name" header="Name"></Column>
      <Column field="category" header="Category"></Column>
      <Column field="quantity" header="Quantity">
        <template #body="{ data }">
          <Button
            class="mr-2"
            icon="pi pi-search"
            @click="selectRow(data)"
            severity="danger"
            rounded
            label="edit"
          ></Button>
          <Button
            icon="pi pi-search"
            @click="deleteUser(data)"
            severity="warn"
            rounded
            label="delete"
          ></Button> </template
      ></Column>
    </DataTable>
  </div>
</template>

<style scoped></style>
