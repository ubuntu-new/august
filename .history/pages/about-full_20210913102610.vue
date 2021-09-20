<template>
<div class="container pl-30 pr-30">
    <div class="row">
        <div class="col-12 aboutFull" style="height: 100px;">
            <span class="about-us">
               {{ about.title }}
            </span>
        </div>
    </div>
    <div class="desktopiza">
        <div class="row ">
            <div class="col-6 sm-12">
                <blockquote>
                    <span class="about-quote">
                        {{ about.quote }}
                    </span>
                </blockquote>

            </div>
            <div class="col-6">
                &nbsp;
            </div>
        </div>

        <div class="row ">
            <div class="col-12">
                <img src="../assets/img/about/august-about-full.jpg" class="mx-auto d-block">
            </div>
        </div>
        <div class="row mt-60 mb-60">
            <div class="col-2  sm-12">
                <span class="about-us">
                {{ about.title }}
            </span>
            </div>
            <div class="col-5" v-html="aboutHalf1">
                
            </div>
            <div class="col-5" v-html="aboutHalf2">
                
            </div>
            <!-- <div class="col-4  sm-12">
         The art of baking was developed early during the Roman Empire. It was a highly famous art as Roman citizens loved baked goods and demanded for them frequently for important occasions such as feasts and weddings etc. Due to the fame and desire that the art of baking received, around 300 BC, baking was introduced as an occupation and respectable profession for Romans.    
        </div> -->
        </div>
    </div>
    <div class="mobiluriza">
        <div class="row ">
            <div class="col-12">
                <blockquote>

                </blockquote>

            </div>
            <div class="col-12">
                <span class="about-quote">
                    {{ about.quote }}
                </span>

            </div>

        </div>

        <div class="row ">
            <div class="col-12">
                <img src="../assets/img/about/august-about-full.jpg" class="mx-auto d-block">
            </div>
        </div>
        <div class="row mb-60">
            <div class="col-4  sm-12">
                <!-- <span class="about-us">
                {{ about.title }}
            </span> -->
            </div>
            <div class="col-12" v-html="aboutHalf1">
                {{ }}
            </div>
            <div class="col-12" v-html="aboutHalf2">
                {{ }}
            </div>
            <!-- <div class="col-4  sm-12">
         The art of baking was developed early during the Roman Empire. It was a highly famous art as Roman citizens loved baked goods and demanded for them frequently for important occasions such as feasts and weddings etc. Due to the fame and desire that the art of baking received, around 300 BC, baking was introduced as an occupation and respectable profession for Romans.    
        </div> -->
        </div>
    </div>

</div>
</template>

<style scoped>


</style>

<script>
import axios from 'axios'
export default {
    data: () => ({
        allABOUT: [],
        about: {},
        aboutHalf1: '',
        aboutHalf2: '',
    }),
    mounted() {
        const lang = this.$store.getters.language;
        const TOKEN = 'RiG7zh-dadLHoih5AeXXzmEbaXvWbHPS';

        // var bodyFormData = new FormData();
        // bodyFormData.set("branch", this.branch);
        // bodyFormData.set("status_key", this.status);

        axios.request({
                method: "post",
                url:
                    // "http://august.webertela.online/rest/web/index.php?r=v1/about/list",
                    "http://localhost/webertela-new/rest/web/index.php?r=v1/about/list",
                headers: {
                    Authorization: "Bearer " + TOKEN,
                },

                // data: bodyFormData,
            })
            .then((response) => {
                console.log('Products Response: ', response);
                this.allABOUT = response.data;
                this.about = this.allABOUT[0];

                if(lang == 'ka'){
                this.allABOUT.forEach((x) => {
                    x.description_en = x.description;
                    x.description = x.description_ge;
                    x.quote_en = x.quote;
                    x.quote = x.quote_ge;
                    x.title_en = x.title;
                    x.title = x.title_ge;
                });
            }





                var s = this.about.description;

                var middle = Math.floor(s.length / 2);
                var before = s.lastIndexOf(' ', middle);
                var after = s.indexOf(' ', middle + 1);

                if (middle - before < after - middle) {
                    middle = before;
                } else {
                    middle = after;
                }

                this.aboutHalf1 = s.substr(0, middle);
                this.aboutHalf2 = s.substr(middle + 1);
            });
    },
}
</script>
