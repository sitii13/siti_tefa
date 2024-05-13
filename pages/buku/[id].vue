<template>
    <div class="container-fluid">
        <h2 class="text-start my-4">{{ buku.judul }}</h2>
        <div class="row">
            <div class="col-md-3">
                <span v-if="buku.cover"><img :src="buku.cover" :alt="buku.judul"/></span>
            </div>
            <div class="col-md-6">
                <div class="badge bg-primary p-2">{{ buku.kategori }}</div>
                <ul class="list-group list-groupflush">
                    <li class="list-group-item">penulis: {{ buku.penulis }}</li>
                    <li class="list-group-item">penerbit: {{ buku.penerbit}}</li>
                    <li class="list-group-item">Tahun terbit : {{ buku.tahun_terbit }}</li>
                    <li class="list-group-item">{{buku.deskipsi}}</li>
                </ul>
             </div>
        <div class="" style="margin-left: 10px;"></div>
        <nuxt-link to="../buku"><button type="submit" class="btn btn-lg btn-dark rounded-5 px-5 bg-primary text-white" style="float: right; margin-bottom: 15px;">KEMBALI</button></nuxt-link>
    </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const route = useRoute();
const buku = ref([]);

const getbookById = async () => {
    const { data, error } = await supabase
    .from('buku')
    .select('*')
    .eq('id', route.params.id)
    .single();
    if(data) buku.value = data
};

onMounted(() => {
    getbookById()
});
</script>