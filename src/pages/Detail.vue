<template>
<div>
  <div style="height:75px">
    
  </div>

  <div class="row">
        <div class="col-8">
          <el-carousel height="500px">
            <div v-for="(o) in gambar" :key="o.id_gambar">
              <el-carousel-item>
                <img class="d-block" v-bind:src="o.url" alt="First slide" width="100%" />
                <div class="carousel-caption d-none d-md-block">
                </div>
              </el-carousel-item>
            </div>

          </el-carousel>
          <hr>
          <div class="col-10">
            <h3>Deskripsi:</h3>
            <p style="min-height:100px">{{kos.description}}</p>
          </div>
        </div>
        <div class="col-4">
          <div class="row"><h1 style="margin-bottom:5px"><b>{{kos.name}}</b></h1></div>
          <div class="row">
            <div class="col-4"><h7 style="display: inline">{{kos.owner}}</h7></div>
          </div>
          <hr class="style1">
          <div class="row">
            <div class="col-2"><h6 style="display: inline">Type:</h6></div>
            <div class="col-9"><h3 class="text-center" style="display: inline" v-if="kos.kos_type === 'L'">Kos putra</h3><h3 class="text-center" style="display: inline" v-if="kos.kos_type === 'P'">Kos putri</h3></div>
          </div>
          <hr class="style1">
          <div class="row">
            <div class="col-2"><h6 style="display: inline">Kontak:</h6></div>
            <div class="col-9"><h3 class="text-center" style="display: inline">{{kos.contact}}</h3></div>
          </div>
          <hr class="style1"> 
          <div class="row">
            <div class="col-2"><h6 style="display: inline">Fasilitas:</h6></div>
            <div class="col-9">
              <div class="row">
                <div class="col-2" v-if="kos.wifi">
                  <div class="row justify-content-md-center"><i class="fas fa-wifi"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">WiFi</div>
                </div>
                <div class="col-2" v-if="kos.bathroom">
                  <div class="row justify-content-md-center"><i class="fas fa-bath"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">KAMAR MANDI DALAM</div>
                </div>
                <div class="col-2" v-if="kos.laundry">
                  <div class="row justify-content-md-center"><i class="fas fa-tshirt"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">LAUNDRY</div>
                </div>
                <div class="col-2" v-if="kos.food">
                  <div class="row justify-content-md-center"><i class="fas fa-utensils"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">MAKAN</div>
                </div>
                <div class="col-2" v-if="kos.m_parking">
                  <div class="row justify-content-md-center"><i class="fas fa-motorcycle"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">PARKIR MOTOR</div>
                </div>
                <div class="col-2" v-if="kos.kitchen">
                  <div class="row justify-content-md-center"><i class="fas fa-blender"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">DAPUR</div>
                </div>
                <div class="col-2" v-if="kos.ac">
                  <div class="row justify-content-md-center"><i class="fas fa-temperature-low"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">AC</div>
                </div>
                <div class="col-2" v-if="kos.tutoring">
                  <div class="row justify-content-md-center" ><i class="fas fa-chalkboard-teacher"></i></div>
                  <div class="row justify-content-md-center" style="font-size:10px;text-align:center">BIMBEL</div>
                </div>
              </div>
            </div>
          </div>
          <hr class="style1">
          <div class="row">
            <div class="col-2"><h6 style="display: inline">Alamat:</h6></div>
            <div class="col-9"><h5 class="text-center" style="display: inline">{{kos.alamat}}</h5></div>
          </div>
          <hr class="style1">
        </div>
  </div>




</div>

</template>
<script>
import { Carousel, CarouselItem } from 'element-ui';

export default {
  name: 'detail',
  bodyClass: 'detail-page',
  components: {
    [Carousel.name]: Carousel,
    [CarouselItem.name]: CarouselItem
  },
  data() {
    return{
      kos : [], 
      gambar: [],
    }
  },
    methods: {
      getData(){
        Vue.axios.get('http://127.0.0.1:8000/api/kos/'+ this.$route.params.id +'/').then((response) => {
            console.log(response.data);
            this.kos = response.data;
            this.gambar = response.data.gambar;
        });

      },
  },
  mounted(){
      this.getData();
  },
};
</script>
<style scoped>
h6{
  color: rgb(112, 112, 112);
}
</style>
