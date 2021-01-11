<template>
<div :class='isDark ? "detailsLightMode" : "detailsDarkMode"' class="detailsOutter ">
    <titleDiv @setMode='getMode'></titleDiv>
    <div class="back">
        <van-button class="backBtn" @click="backList" size="small" icon="arrow-left">
            back
        </van-button>
    </div>
    <div class="content">
        <div class="flag">
            <van-image
                fit='cover'
               
                :src='info.flag'
            />
        </div>
        <div class="info">
            <div class="name">{{info.name}}</div>
            <div class="two">Native Name: {{info.nativeName}}</div>
            <div class="two">Top Level Domain: <span v-for="(item ,index) in info.topLevelDomain" :key="index">{{item}}</span></div>
            <div class="three">Population: {{info.population}}</div>
            <div class="three">Currencies: <span v-for="(item ,index) in info.currencies" :key="index">{{item.name}}</span></div>
            <div class="four">Region: {{info.region}}</div>
            <div class="four">Languages: <span v-for="(item ,index) in info.languages" :key="index">{{item.name}}</span></div>
            <div class="five">Sub Region: {{info.subregion}}</div>
            <div class="six">Capital: {{info.capital}}</div>
            <div class="seven">Borders Countries： <div class="btnDiv"><van-button @click="searchInfo(item)" class="countries" size="mini" v-for="(item, index) in info.borders" :key="index">{{item}}</van-button></div></div>
        </div>
    </div>
</div>
</template>

<script>
import titleDiv from '../../components/title'
import Button from 'vant/lib/button';
import 'vant/lib/popover/style';
import Image from 'vant/lib/image';
import 'vant/lib/image/style';

export default {
    components: {
        titleDiv,
        [Button.name]: Button,
        [Image.name]: Image
    },
    data () {
        return {
            isDark: false,
            info: Object
        }
    },
    created () {
        this.$http.get('https://restcountries.eu/rest/v2/alpha/' + this.$route.query.code).then((response) => {
            this.info = response.data
        })
    },
    methods: {
        getMode (val) {
            this.isDark = val
        },
        searchInfo (item) {
            this.$http.get('https://restcountries.eu/rest/v2/alpha/' + item).then((response) => {
                this.info = response.data
            })
        },
        backList () {
             this.$router.push({
                path: '/'
            })
        }
    }
}
</script>

<style lang="less" scoped>
.detailsDarkMode{
    background-color: hsl(207, 26%, 17%);
    color: hsl(0, 0%, 98%);;
    /deep/ .van-button--default {
        color: hsl(0, 0%, 100%);
        background-color: hsl(209, 23%, 22%);
        border: 1px solid hsl(207, 26%, 17%);
    }
}
.detailsLightMode{
    background-color:  hsl(0, 0%, 98%);
    color:  hsl(200, 15%, 8%);
    /deep/ .van-button--default {
        color:  hsl(200, 15%, 8%);
        background-color: hsl(0, 0%, 100%);
        border: 1px solid hsl(0, 0%, 98%);
    }
}
@media screen and (max-width: 376px) {
    .detailsOutter{
        height: 100vh;
        overflow: auto;
    }
    .back{
        padding: 30px 0 40px 20px;
        text-align: left;
    }
    /deep/ .van-image{
        width: 82vw;
        height: 50vw;
    }
    .info{
        text-align: left;
        padding-left: 30px;
        .name{
            height: 80px;
            line-height: 80px;
            font-size: 26px;
            font-weight: 600;
        }
        height: 35px;
        line-height: 35px;
    }
    .countries{
        margin-right: 10px;
        margin-bottom: 10px;
    }
    /deep/ .van-button--mini+.van-button--mini{
        margin-left: 0;
    }
}
@media screen and (min-width: 1440px) {
    .btnDiv{
        display: inline-block;
    }
    .detailsOutter{
        height: 100vh; 
    }
    .back{
        padding: 70px 60px;
        text-align: left;
    }
    /deep/ .van-image{
        width: 35vw;
        height: 20vw;
    }
    .content{
        height: calc(100vh - 242px);
        display: flex;
        .flag, .info{
            padding-left: 180px;
        }
        .info{
            text-align: left;
            .name{
                height: 80px;
                line-height: 80px;
                font-size: 26px;
                font-weight: 600;
            }
            .two, .three, .four{
                display: inline-block;
                width: 50%;
            }
            height: 35px;
            line-height: 35px;
        }
    }
    .countries{
        margin-left: 10px;
    }
}
</style>