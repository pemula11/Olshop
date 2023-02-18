<template>
  <div class="home">
      <HeaderOlshop/>
      <HeroOlshop/>
      <BannerOlshop/>
      <InstaOlshop/>
      <PartnertOlshop/>
      <FooterOlshop/>

       <!-- Hero Section Begin -->
    
      <!-- Hero Section End -->
  </div>


  
</template>



<script lang="js">
// @ is an alias to /src
//import HelloWorld from '@/compo
import HeaderOlshop from '@/components/HeaderOlshop.vue';
import HeroOlshop from '@/components/HeroOlshop.vue';
import BannerOlshop from '@/components/BannerOlshop.vue';
import InstaOlshop from '@/components/InstaOlshop.vue';
import PartnertOlshop from '@/components/PartnertOlshop.vue';
import FooterOlshop from '@/components/FooterOlshop.vue';

export default {
  name: 'HomeView',
  components: {
   
    HeaderOlshop,
    HeroOlshop,
    BannerOlshop,
    InstaOlshop,
    PartnertOlshop,
    FooterOlshop,
  }
}
</script>
