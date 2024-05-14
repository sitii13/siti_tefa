<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">BUKU</h2>
        <div class="my-3">
          <form @submit.prevent="getbooks">
          <input v-model="keyword" type="search" class="form-control rounded-5 mb-3 " placeholder="Mau Baca apa hari ini?" />
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan {{ books.length }} dari {{ books.length }} buku </div>
        <div class="row">
          <div v-for="(book,i) in books" :key="i" class="col-lg-2">
              <div class="card mb-3">
                <nuxt-link :to="`buku/${book.id}`">
                  <div class="card-body">
                    <img :src="book.cover" class="cover" :alt="book.judul" />
                  </div>
                </nuxt-link>
            </div>
          </div>
        </div>
      </div>
      <nuxt-link to="../"><button type="submit" class="btn btn-lg btn-dark rounded-5 px-5 bg-primary text-white" style="float: right; margin-bottom: 15px;">KEMBALI</button></nuxt-link>
    </div>
  </div>
</template>

<script setup>
useHead({title:'aplikasi perpus digital', 
  meta:[{name:'description', content:'detail buku'}]
})
const supabase = useSupabaseClient();
const keyword = ref("");

const books = ref([]);

const getbooks = async () => {
  const { data, error } = await supabase.from("buku").select(`*, kategori(*)`).ilike("judul", `%${keyword.value}%`)
  if(data) books.value = data;
}
onMounted(() => {
  getbooks();
});
</script>

<style scoped>
.card-body {
  width: 100%;
  height: 30em;
  padding: 0;
}
.cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}
</style>

