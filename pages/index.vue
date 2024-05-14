<template>
  <div class="container-fluid">
    <div class="row my-5 justify-content-around mt-5">
      <div class="col-lg-5">
        <nuxt-link to="/pengunjung/tambah">
          <div class="card bg-pengunjung rounded-5" style="height: 350px;">
            <div class="card-body">
              <h2>pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>

      <div class="col-lg-5 ">
        <nuxt-link to="/buku">
          <div class="card bg-buku rounded-5" style="height: 350px;">
            <div class="card-body">
              <h2>Cari Buku</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
      
    <div class="mt-5" style="margin-left : 200px">
      <h2 class=" " >STATISTIK</h2>
    </div>

        <div class="row my-5 justify-content-around" style="margin-right: 20px">
          <div class="col-lg-5">
            <div class="card bg-spengunjung rounded-5" style="height: 350px;">
              <div class="card-body">
                <nuxt-link to="/pengunjung">
                  <div class="row">
                <div class="col p-5" ><h1 style="font-size: 120px">{{ jumlahp }}</h1></div>
                <div class="col mt-5 p-5" style="margin-left :-200px"><h2>pengunjung</h2></div>
              </div>
                </nuxt-link>
          </div>
        </div>
      </div>

      <div class="col-lg-5">
        <div class="card bg-sbuku rounded-5 ms-4" style="height: 350px;">
          <div class="card-body">
            <nuxt-link to="/buku">
              <div class="row">
                <div class="col p-5"><h1 style="font-size: 120px; margin-right: 200px;">{{ jumlahp }}</h1></div>
                <div class="col mt-5 p-5"><h2 >Buku</h2></div>
              </div>
            </nuxt-link>
            </div>
          </div>
        </div>
      </div>
    </div>
    <chart/>
  </div>
</template>

<script setup>
useHead({title:'aplikasi perpus digital', 
  meta:[{name:'description', content:'selamat datang di perpus digital SMKN 4'}]
})
const supabase = useSupabaseClient();
const jumlahp = ref(0);
const jumlahb =ref(0);

async function ambiljumlahp () {
  const { data, error, count } =await supabase
  .from("pengunjung")
  .select("*", {count: "exact"});
  if (count) jumlahp.value = count;
};

async function ambiljumlahb () {
  const { data, error, count } =await supabase
  .from("pengunjung")
  .select("*", {count: "exact"});
  if (count) jumlahb.value = count;
};

onMounted(() =>{
  ambiljumlahb();
  ambiljumlahp();
});
</script>

<style scoped>
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #424242;
}
.card.bg-pengunjung {
  background-image: url("../assets/img/kunjungan.jpeg");
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  color: black;
  opacity: 70%;
}
.card.bg-buku {
  background: url('../assets/img/bg-home-cari-buku.jpg')no-repeat center center;
  background-size: cover;
  color: black;
  opacity: 70%;
}
.card.bg-spengunjung {
  background-color: #E9E236;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  opacity: 70%;
  
}
.card.bg-sbuku {
background-color: #69B4AF;
background-repeat: no-repeat;
background-position: center center;
background-size: cover;
opacity: 70%;
}
</style>