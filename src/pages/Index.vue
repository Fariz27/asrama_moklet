<template>
  <div>
    <div class="page-header clear-filter" filter-color="orange">
      <parallax
        class="page-header-image"
        style="background-image:url('img/header.jpg')"
      >
      </parallax>
      <div class="container">
        <div class="content-center brand">
          <img class="n-logo" src="img/now-logo.png" alt="" />
          <h1 class="h1-seo">Asrama Moklet</h1>
            <fg-input placeholder="Cari Kos Di Sini" v-model="search" v-on:keyup.enter="searching">
            </fg-input>
          <h3>Cari Kos Ternyaman dan Terbaik Disini !</h3>
          <div>
          </div>
        </div>
      </div>
    </div>
    <div class="main">
      <div class="section section-images">
        <div class="container">
          <div class="row">
            <div class="col-md-12">
              <div class="hero-images-container">
                <img src="img/hero-image-1.png" alt="" />
              </div>
              <div class="hero-images-container-1">
                <img src="img/hero-image-2.png" alt="" />
              </div>
              <div class="hero-images-container-2">
                <img src="img/hero-image-3.png" alt="" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <button type="button" v-on:click="refresh" class="btn btn-info" style="margin-left: 5%;font-size:1.5em">Refresh</button>
    <div class="row" style="min-height:500px">
      <ContentCard v-if="contentCardOn"></ContentCard>
    </div>
  </div>
</template>
<script>
import { Parallax } from '@/components';
import {
  Button,
  Checkbox,
  Radio,
  FormGroupInput,
  Slider,
  Switch
} from '@/components';
import ContentCard from './components/ContentCard';

import BasicElements from './components/BasicElementsSection';
import Navigation from './components/Navigation';
import TabsSection from './components/Tabs';
import ProgressPagination from './components/ProgressPagination';
import Notifications from './components/Notifications';
import Typography from './components/Typography';
import JavascriptComponents from './components/JavascriptComponents';
import CarouselSection from './components/CarouselSection';
import NucleoIconsSection from './components/NucleoIconsSection';
import SignupForm from './components/SignupForm';
import ExamplesSection from './components/ExamplesSection';
import DownloadSection from './components/DownloadSection';
import axios from 'axios';

// -----------------------------------------------------------------------------------

export default {
  name: 'index',
  bodyClass: 'index-page',
  components: {
    ContentCard,

    Parallax,
    BasicElements,
    Navigation,
    TabsSection,
    ProgressPagination,
    Notifications,
    Typography,
    JavascriptComponents,
    CarouselSection,
    NucleoIconsSection,
    SignupForm,
    ExamplesSection,
    DownloadSection,
    [Button.name]: Button,
    [Checkbox.name]: Checkbox,
    [Radio.name]: Radio,
    [FormGroupInput.name]: FormGroupInput,
    [Switch.name]: Switch,
    [Option.name]: Option,
    Slider
  },
  data(){
    return{
      search:"",
      temp_search:"",
      contentCardOn: true,
    }
  },
  methods: {
    searching(){
      this.$router.push('/search/'+this.search);
      console.log("BERHASIl");
      this.refresh();
    },
    refresh(){
      this.contentCardOn=false;
      this.$nextTick(() => {
        this.contentCardOn = true;
      });      
    }
  }

};
</script>
<style></style>
