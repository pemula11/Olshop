

<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5">
                    <carousel :items-to-show="3">
                        <slide v-for="slide in 10" :key="slide">
                            <div class="product-item">
                                <div class="pi-pic">
                                    <img src="img/mickey1.jpg" alt="" />
                                    <ul>
                                        <li class="w-icon active">
                                            <a href="#"><i class="icon_bag_alt"></i></a>
                                        </li>
                                        <li class="quick-view">
                                            <router-link to="/product">
                                                Quick View
                                            </router-link>
                                        </li>
                                    </ul>
                                </div>
                                <div class="pi-text">
                                    <div class="catagory-name">Coat</div>
                                    <router-link to="/product">
                                        <a href="#">
                                          <h5>Mickey Baggy</h5>
                                         </a>
                                    </router-link>
                                    
                                    <div class="product-price">
                                        $14.00
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
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

  

<script>
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'


    export default {
        name: 'BannerOlshop',
        components: {
            Carousel,
            Slide,
            Pagination,
            Navigation,
        }
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