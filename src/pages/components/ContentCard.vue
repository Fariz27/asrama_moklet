<template>
 <div style="margin-left: 5%;margin-right: 5%;">
       <div class="row">
         <div class="col-md-3" :span="6" v-for="(o) in kos" :key="o.id">
             <el-card style="margin:20px;font-size:2vw " :body-style="{ padding: '1px' }">
             <img v-bind:src="o.url" class="image">
             <div style="padding: 14px;">
                 <span class="titleFont">{{o.name}}</span>
                 <div class="bottom clearfix">
                   <p style="font-size:1vw" v-if="o.description.length<81">{{o.description}}</p>
                   <p style="font-size:1vw" v-else>{{o.description.substring(0,81)+". . . ."}}</p>
                 <h2 class="harga" style="font-size:1.5vw">{{o.alamat}}</h2>
                 <router-link v-popover:popover1 class="navbar-brand" :to="{ name: 'detail', params: { id: o.id }}">
                 Detail
                 </router-link>
                 <el-button type="text" class="button"></el-button>
                 </div>
             </div>
             </el-card>
         </div>
     </div>
      <nav aria-label="Page navigation example">
        <ul class="pagination justify-content-center">
          <li class="page-item"><a class="page-link" v-on:click="paginationDown">Previous</a></li>
          <li class="page-item"><a class="page-link" v-on:click="paginationUp">Next</a></li>
        </ul>
      </nav>
 </div>

</template>
<script>
import Vue from 'vue';
window.Vue = Vue;
import { Card, Button} from 'element-ui';
export default {
  name: 'ContentCard',
  data() {
    return {
      kos : [], 
      paginationArr : [],
      perPage : 10,
      currentPage : 1,
      isSearch: "",
      dataCount: 0,
    };
  },
  components: {
    [Button.name]: Button,
    [Card.name]: Card,


  },
  methods: {
      getData(){
            if(typeof this.$route.params.search == "undefined" || this.$route.params.search == null){
              Vue.axios.get('http://127.0.0.1:8000/api/kos/'+this.perPage+'/'+((this.currentPage-1)*10)).then((response) => {
                  console.log(response.data);
                  this.kos = response.data.kos;
                  this.dataCount = response.data.count;
                  console.log(this.kos);
                  console.log(this.dataCount);
                  this.dataCount = this.dataCount/this.perPage;
                  this.dataCount = parseInt(this.dataCount, 10);
                  console.log(this.dataCount);


              });
            }else{
              this.searching();
            }
      },
      searching(){
        Vue.axios.post('http://127.0.0.1:8000/api/kos/search',{
          find: this.$route.params.search,
        }).then((response) => {
            console.log(response.data);
            this.kos = response.data.kos;
            console.log(this.kos);
        });

      },
      paginationUp(){
        if(this.currentPage<=this.dataCount){
          this.currentPage = this.currentPage+1;
          this.getData();          
          console.log(this.currentPage);
        }

      },
      paginationDown(){
        if(this.currentPage>0){
          this.currentPage -= 1
        this.getData();          
        }


      }
  },
  mounted(){
      this.getData();
  },
};
</script>
<style>
  .titleFont{
    font-size: 2vw;
  }
  .harga{
    font-size: 2.5vw;
  }
  .time {
    font-size: 13px;
    color: #999;
  }
  
  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .button {
    padding: 0;
    float: right;
  }

  .image {
    width: 100%;
    display: block;
  }

  .clearfix:before,
  .clearfix:after {
      display: table;
      content: "";
  }
  
  .clearfix:after {
      clear: both
  }

</style>




