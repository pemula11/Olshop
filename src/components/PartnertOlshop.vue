<template>
    <div>
    <!-- Partner Logo Section Begin -->
        <div class="partner-logo">
            <div class="container">
                <carousel :items-to-show="3" :wrap-around="true" :autoplay=1000>
                    <slide v-for="slide in 10" :key="slide">
                        <div class="logo-item">
                            <div class="tablecell-inner">
                                <img src="img/logo-carousel/logo-1.png" alt="" />
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
    <!-- Partner Logo Section End -->

    </div>
</template>


<script>
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'
    export default {
        name: "PartnertOlshop",
        components: {
            Carousel,
            Slide,
            Pagination,
            Navigation,
        }
    }
</script>