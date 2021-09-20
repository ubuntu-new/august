<template>
<div class="racxa">

    <div class="products-filter-options">
        <div class="row align-items-center">
            <div class="col d-flex">
            </div>
        </div>
    </div>

    <div class="container shopCOntainer">

        <div id="products-filter" class="products-collections-listing row">
            <ProductItem v-for="(product, index) in filteredOrders" :product="product" :key="index" @clicked="toggle" :className="`col-md-4 products-col-item`"></ProductItem>
        </div>
    </div>
</div>
</template>

<style scoped>

</style>

<script>
import QuckView from '../modals/QuckView';
import axios from 'axios';
import {
    mutations
} from '../../utils/sidebar-util';
import ProductItem from '../landing-one/ProductItem.vue';
export default {
    data() {
        return {
            allProducts: []
        }
    },
    components: {
        QuckView,
        ProductItem
    },
    props: ['category', 'catList'],
    methods: {
        toggle() {
            mutations.toggleQuickView();
        }
    },
    mounted() {
        const TOKEN = 'RiG7zh-dadLHoih5AeXXzmEbaXvWbHPS';

        axios.request({
            method: "post",
            url:
            "http://localhost/webertela-new/rest/web/index.php?r=v1/products/list",
            headers: {
            Authorization: "Bearer " + TOKEN,
            },
            // data: bodyFormData,
        })
        .then((response) => {
            console.log('Products Response: ', response);
            this.allProducts = response.data;
            this.allProducts.forEach((x) => {
                x.qty = 1;
                if(x.filePath === null){
                    x.filePath = 'placeHolder.png';
                },
                if (lang == 'ka') {
                    console.log('Catogeries Response: ', response);
                    this.allNews = response.data;
                    this.allNews.forEach((x) => {
                        x.title_en = x.title,
                            x.title = x.title_ge,
                            x.description_en = x.description,
                            x.description = x.description_ge,
                            x.name = x.name_ge,
                    });
                    this.featuredNews = this.allNews.filter((x) => x.feautured == '1');
                    console.log('featured: ', this.featuredNews);
                } else {
                    console.log('Catogeries Response: ', response);
                    this.allNews = response.data;
                    this.featuredNews = this.allNews.filter((x) => x.feautured == '1');
                    console.log('featured: ', this.featuredNews);
                }
            });
                
            });
        
    },
    computed: {
        products() {
            return this.$store.state.products.all
        },
        filteredOrders(){
            if(this.category.id == -1){
                console.log('categories list: ', this.catList);
                return this.allProducts;
            }
            else {
                return this.allProducts.filter((x) => 
                    x.catId == this.category.id
                );
            }
        },
    },
}
</script>
