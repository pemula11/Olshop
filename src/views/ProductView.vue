<template>
    <div class="home">
        <HeaderOlshop/>

   <!-- Breadcrumb Section Begin -->
   <div class="breacrumb-section text-left">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more">
                        
                        <router-link to="/">
                            <i class="fa fa-home"></i> Home
                        </router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="gambar_default" alt="" />
                            </div>
                            <div class="product-thumbs" >
                                <carousel :items-to-show="3" :autoplay=3000>
                                    <slide v-for="img in productDetails.galleries" :key="img.id">
                                        <div class="pt" 
                                        v-bind:class="img.default == gambar_default ? 'active' : ''" @click="changeImage(img.photo)">
                                         <img :src="img.photo" alt="" />
                                        </div>
                                    </slide>
                                    <template #addons>
                                        <navigation />
                                        <pagination />
                                    </template>

                                </carousel>
                            </div>
                           
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{productDetails.type}}</span>
                                    <h3>{{productDetails.name}}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p v-html="productDetails.description">
                                      
                                  

                                    </p>
                                    
                                    <h4>Rp. {{productDetails.price}}</h4>
                                </div>
                                <div class="quantity">
                                    <router-link to="/cart">
                                        <a @click="saveKeranjang(productDetails.id, productDetails.name, productDetails.galleries[0].photo, productDetails.price)"  class="primary-btn pd-card">Add To Cart</a>
                                    </router-link>
                                    
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->


        <RelatedOlshop/>
        <FooterOlshop/>
  
        
    </div>
  
  
    
  </template>
  
  
  
  <script lang="js">
  // @ is an alias to /src
  //import HelloWorld from '@/compo
  import HeaderOlshop from '@/components/HeaderOlshop.vue';
  import RelatedOlshop from '@/components/RelatedOlshop.vue';
  import FooterOlshop from '@/components/FooterOlshop.vue';
  import axios from "axios";

  import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'
  
  export default {
    name: 'ProductView',
    components: {
     
      HeaderOlshop,
      FooterOlshop,
      RelatedOlshop,
      Carousel,
      Slide,
      Pagination,
      Navigation,
    }, 
    data(){
        return {
            gambar_default: "",
            productDetails: [],
            keranjangUser: [],
        }
    },
    methods: {
        changeImage(urlImage){
            this.gambar_default = urlImage
            //eslint-disable-next-line no-console
            
        },
        setDataPicture(data){
            this.productDetails = data;
            this.gambar_default = data.galleries[0].photo;
        },
        saveKeranjang(idProduct, nameProduct, photoProduct, priceProduct){
            var productStored = {
                "id": idProduct,
                "name": nameProduct,
                "photo": photoProduct,
                "price": priceProduct,
            }
            this.keranjangUser.push(productStored);
            let parsed = JSON.stringify(this.keranjangUser)
            localStorage.setItem('keranjangUser', parsed)
        }
    },
    
    mounted() {
        if (localStorage.getItem('keranjangUser')){
                try{
                    this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
                } catch(e) {
                    localStorage.removeItem('keranjangUser');
                }
        }
        axios
            .get("http://olshop-backend.test/api/products", {
                params: {
                    id: this.$route.params.id,
                }
            })
            .then(res => (this.setDataPicture(res.data.data)))
            //this.productDetails = res.data.data

            .catch(err => console.log(err));
        },
        
  }
  </script>
  
<style>
    .product-thumbs .pt {
        margin-right: 10px;
    }
</style>
