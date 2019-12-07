<template>
  <div class="page-header clear-filter" filter-color="orange">
    <div
      class="page-header-image"
      style="background-image: url('img/login.jpg')"
    ></div>
    <div class="content">
      <div class="container">
        <div class="col-md-5 ml-auto mr-auto">
          <card type="login" plain>
            <div slot="header" class="logo-container">
              <img v-lazy="'img/now-logo.png'" alt="" />
            </div>
            <form v-on:submit.prevent="Login">
              <fg-input
                class="no-border input-lg"
                addon-left-icon="now-ui-icons users_circle-08"
                id="email"
                v-model="email"
                placeholder="Email"
                required
                autofocus
                tabindex="1"                
              >
              </fg-input>

              <fg-input
                class="no-border input-lg"
                addon-left-icon="now-ui-icons text_caps-small"
                id="password"
                v-model="password"
                type="password"
                placeholder="Password"
                required
                tabindex="2"
              >
              </fg-input>
              <div class="card-footer text-center">
                <button
                  type="submit"
                  href="#pablo"
                  class="btn btn-primary btn-round btn-lg btn-block"
                  tabindex="4"
                  pill
                  >LOGIN
                </button
                >
              </div>
            </form>
            <template slot="raw-content">
              <div class="pull-left">
                <h6>
                  <a href="#pablo" class="link footer-link">Create Account</a>
                </h6>
              </div>
              <div class="pull-right">
                <h6>
                  <a href="#pablo" class="link footer-link">Need Help?</a>
                </h6>
              </div>
            </template>
          </card>
        </div>
      </div>
    </div>
    <main-footer></main-footer>
  </div>
</template>
<script>
import { Card, Button, FormGroupInput } from '@/components';
import MainFooter from '@/layout/MainFooter';
export default {
  name: 'login-page',
  bodyClass: 'login-page',
  components: {
    Card,
    MainFooter,
    [Button.name]: Button,
    [FormGroupInput.name]: FormGroupInput
  },
  data() {
    return {
      email: "",
      password: "",
      message: "Mohon tunggu...",
      type: "secondary",
      show: false,
      spin: false,
    };
  },
  methods: {
      authenticate : function(){
        if(this.$cookies.isKey("Authorization")){
          let conf = { headers : {"Authorization" : "Bearer " + this.$cookies.get("Authorization")} };
          axios.get(base_url + "/user/check", conf)
          .then(response => {
            if(response.data.auth == true){
              console.log("auth");
            }
          })
          .catch(error => {
            console.log(error);
          });
        }
      },
      Login: function(){
        this.message = "Mohon tunggu...";
        let form = new FormData();
        form.append("email", this.email);
        form.append("password", this.password);
        Vue.axios.post("http://127.0.0.1:8000/api/login").then((response) => {
          let logged = response.data.logged;
          if(logged){
              if(this.$cookies.isKey("Authorization")){
                  this.$cookies.remove("Authorization");
              }
              this.$cookies.set("Authorization", response.data.token);
              this.type = "success";
              this.message = "Berhasil login";
              router.push("index");
          } else {
              this.type = "danger";
              this.message = "email atau password salah";
          }
          console.log(message);
        });
        //   let logged = response.data.logged;
        //   if(logged){
        //       if(this.$cookies.isKey("Authorization")){
        //           this.$cookies.remove("Authorization");
        //       }
        //       this.$cookies.set("Authorization", response.data.token);
        //       this.type = "success";
        //       this.message = "Berhasil login";
        //       router.push("index");
        //   } else {
        //       this.type = "danger";
        //       this.message = "email atau password salah";
        //   }
        //   console.log(message);
        // });
        console.log(this.email);
        console.log(this.password);

      }
    },
    mounted(){
      this.authenticate();
    }
};
</script>
<style></style>
