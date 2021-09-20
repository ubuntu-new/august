<template>
<client-only>
    <div class="">
        <div class="AboutMain desktopiza">
            <div class="row h-100">
                <div class="patara border-right border-top">&nbsp;</div>
                <div class="sashualo border-right border-top">&nbsp;</div>
                <div class="sashualo border-right border-top">&nbsp;</div>
                <div class="didi border-right border-top">
                    <span class="cifraTitle">
                        01
                    </span>
                </div>
                <div class="patara border-right border-top">&nbsp;</div>
            </div>
            <div class="row">
                <div class="patara border-right border-top">&nbsp;</div>
                <div class="sashualo border-right border-top h-500 relative">
                    <img src="img/about/about-first.jpg" class="one  absolute">
                </div>
                <div class="sashualo border-right border-top h-500 relative">
                    <img src="img/about/about-second.jpg" class="two absolute">
                </div>
                <div class="didi border-right border-top relative">
                    <div class="my-auto text-left aboutiza realtive">
                        <!-- <h1 class="title">{{ about.title }}</h1> -->
                        <h1 class="title">About Us</h1>
                        <p v-html="aboutHalf1"></p>
                        <img src="img/group-2-copy.png" style="float:left">
                        <div class="text-left" style="padding: 0 0 0 80px;">
                            <nuxt-link to="/about-full" style="float: left;
                                                        font-family: Montserrat;
                                                        font-size: 16px;
                                                        font-weight: 300;
                                                        font-stretch: normal;
                                                        font-style: normal;
                                                        line-height: 1.63;
                                                        letter-spacing: normal;
                                                        color: #f8f8f8;
                                                        padding: 12px 20px;">Explore more
                            </nuxt-link>
                        </div>
                        <img src="img/group-94.png" class="Group-94">
                    </div>

                </div>
                <div class="patara border-right border-top">&nbsp;</div>
            </div>
            <div class="row" style="height:80px;">
                <div class="patara border-right border-top">&nbsp;</div>
                <div class="sashualo border-right border-top">&nbsp;</div>
                <div class="sashualo border-right border-top">&nbsp;</div>
                <div class="didi border-right border-top">&nbsp;</div>
                <div class="patara border-right border-top">&nbsp;</div>
            </div>
        </div>

        <div class="AboutMain mobiluriza" style="min-height:150px;">
            <div class="aboutInner">
                <div class="row h-100" style="margin-bottom:-50px">
                    <div class="col-sm-12 border-right border-top">
                        <span class="cifraTitle">
                            01
                        </span>
                    </div>
                    <div class="col-sm-12">
                        <div class="relative">
                            <img src="img/about/about-first.jpg" class="one absolute">
                            <img src="img/about/about-second.jpg" class="two absolute">
                        </div>
                    </div>
                </div>
                <div class="row ">
                    <div class="col-sm-12 aboutiza h-100 ">
                        <h1 class="title">About Us</h1>
                        <p v-html="aboutHalf1"></p>
                    </div>
                    <img src="img/group-2-copy.png" style="float:left">
                        <div class="text-left" style="padding: 0 0 0 80px;">
                            <nuxt-link to="/about-full" style="float: left;
                                                        font-family: Montserrat;
                                                        font-size: 16px;
                                                        font-weight: 300;
                                                        font-stretch: normal;
                                                        font-style: normal;
                                                        line-height: 1.63;
                                                        letter-spacing: normal;
                                                        color: #f8f8f8;
                                                        padding: 12px 20px;">Explore more
                            </nuxt-link>
                        </div>
                        <img src="img/group-94.png" class="Group-94">

                </div>
                <div class="row">
                    <div class="col-sm-12 xorbali">
                                            </div>
                </div>
            </div>

            <!-- <table class="table table-bordered webetrla-table  " CELLPADDING=0 CELLSPACING=0>
                <tbody>
                    <tr>
                        <td colspan="3">
                            <div class="container padding-none">
                                <table class="table " style="height: 80px; position: relative;">
                                    <tbody>
                                        <tr>
                                            <td style="width:25%;">&nbsp;</td>
                                            <td>&nbsp;</td>
                                            <td style="width:50%">
                                                <span class="cifraTitle">

                                                    01

                                                </span>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td colspan="3">
                                                <img src="img/about/about-first.jpg" class="one img-fluid">
                                                <img src="img/about/about-second.jpg" class="two img-fluid">
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table> -->

        </div>
    </div>

</client-only>
</template>

<style scoped>
.h-500 {
    height: 500px;
}

.left {
    position: relative;
    margin: 80px 0 !important;

}

.padding-none {
    padding: 0px;
}
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
        const TOKEN = 'RiG7zh-dadLHoih5AeXXzmEbaXvWbHPS';

        axios.request({
                method: "post",
                // url: "http://august.webertela.online/rest/web/index.php?r=v1/about/list",
                url: "http://localhost/webertela-new/rest/web/index.php?r=v1/about/list",
                headers: {
                    Authorization: "Bearer " + TOKEN,
                },

                // data: bodyFormData,
            })
            .then((response) => {
                console.log('about Response: ', response);
                this.allABOUT = response.data;
                this.about = this.allABOUT[0];

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
    }
}
</script>
