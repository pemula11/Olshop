

<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="products.length > 0">
                    <carousel :items-to-show="3">
                        <slide v-for="itemProduct in products" :key="itemProduct.id">
                            <div class="product-item">
                                <div class="pi-pic">
                                    <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                                    <ul>
                                        <li 
                                        @click="saveKeranjang(itemProduct.id, itemProduct.name, itemProduct.galleries[0].photo, itemProduct.price)"
                                        class="w-icon active">
                                            
                                            <a href="#" >
                                                <i class="icon_bag_alt"></i>
                                            </a>
                                        </li>
                                        <li class="quick-view">
                                            <router-link v-bind:to="'/product/'+itemProduct.id">
                                                Quick View
                                            </router-link>
                                        </li>
                                    </ul>
                                </div>
                                <div class="pi-text">
                                    <div class="catagory-name">{{itemProduct.type}}</div>
                                    <router-link to="/product">
                                        <a href="#">
                                          <h5>{{itemProduct.name}}</h5>
                                         </a>
                                    </router-link>
                                    
                                    <div class="product-price">
                                        Rp. {{itemProduct.price}}
                                        <span>$35.00</span>
                                    </div>
                                </div>
                            </div>
                        </slide>
                        <template #addons>
                            <navigation />
                            <pagination />
                        </template>
                        
                    </carousel>
                </div>
                <div class="col-lg-12" v-else>
                    <p>Produk belum tersedia</p>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

  

<script>
import 'vue3-carousel/dist/carousel.css';
import axios from "axios";

import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'


    export default {
        name: 'BannerOlshop',
        components: {
            Carousel,
            Slide,
            Pagination,
            Navigation,
        },
        data() {
            return {
                products: [],
                keranjangUser: [],
            };
        },
        methods: {
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
            .get("http://olshop-backend.test/api/products")
            .then(res => (this.products = res.data.data.data))

            .catch(err => console.log(err));
        },
    }
</script>



<style scoped>
.product-item {
  margin-right: 25px;
}
.pi-pic img {
  height: 450px;
}
</style>