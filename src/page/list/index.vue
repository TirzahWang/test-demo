<template>
  <div class="" :class='isDark ? "lightMode" : "darkMode"'>
      <titleDiv @setMode='getMode'></titleDiv>
      <operation @setSearch='getSearch' :isDark='isDark' @setScreening='getScreening'></operation>
      <div class="list">
        <div class="boardOutter" @click="goDetails(item.alpha3Code)" v-for="item in list" :key="item.numericCode">
            <van-image
                fit='cover'
                lazy-load
                :src="item.flag"
            />
            <div class="text">
                <div class="name">{{item.name}}</div>
                <div class="textTitle">population: {{item.population}}</div>
                <div class="textTitle">region: {{item.region}}</div>
                <div class="textTitle">capital: {{item.capital}}</div>
            </div>
        </div>
      </div>
  </div>
</template>

<script>
import titleDiv from '../../components/title'
import operation from '../../components/operation'
import Image from 'vant/lib/image';
import 'vant/lib/image/style';
import Vue from 'vue';
import { Lazyload } from 'vant';

Vue.use(Lazyload);

export default {
    components: {
        titleDiv,
        [Image.name]: Image,
        operation
    },
    data () {
        return {
            list: [],
            screening: String,
            search: String,
            isDark: false
        }
    },
    watch: {
        'screening': {
            handler (newV) {
                this.$http.get('https://restcountries.eu/rest/v2/region/' + newV).then((response) => {
                    this.list = response.data
                })
            }
        },
        'search': {
            handler (newV) {
                this.$http.get('https://restcountries.eu/rest/v2/name/' + newV).then((response) => {
                    this.list = response.data
                })
            }
        }
    },
    methods: {
        getMode (val) {
            this.isDark = val
        },
        goDetails (code) {
            this.$router.push({
                path: '/details',
                query: {
                    code: code
                }
            })
        },
        getScreening (val) {
            this.screening = val
        },
        getSearch (val) {
            this.search = val
        }
    }, 
    created () {
        this.$http.get('https://restcountries.eu/rest/v2/all').then((response) => {
            this.list = response.data
        })
    }
}
</script>

<style lang="less" scoped>

@media screen and (max-width: 376px) {
    .list{
        min-height: calc(100vh - 226px); 
    }
    /deep/ .van-image{
        width: 100%;
        margin: 0 auto;
        .van-image__img{
            border: 1px;
            border-radius: 5px 5px 0 0;
        }
    }
   
    .darkMode{
        background-color: hsl(207, 26%, 17%);
        .boardOutter{
            width: 80%;
            margin: 0 auto 40px;
            background-color:  hsl(209, 23%, 22%);
            color: hsl(0, 0%, 98%);;
            border: 1px solid hsl(209, 23%, 22%);
            border-radius: 5px;
        }
    }
    .lightMode{
        background-color: hsl(0, 0%, 98%);
        .boardOutter{
            width: 80%;
            margin: 0 auto 40px;
            background-color:  hsl(0, 0%, 100%);
            color: hsl(200, 15%, 8%);
            border: 1px solid  hsl(0, 0%, 98%);
            border-radius: 5px;
        }
    }
    .text{
        padding-bottom: 30px;
        text-align: left;
        .name{
            height: 50px;
            line-height: 50px;
            font-size: 18px;
        }
        .textTitle{
            height: 30px;
            line-height: 30px;
            font-size: 14px; 
        }
        div{
            padding-left: 30px;
        }
    }
}
@media screen and (min-width: 1440px) {
    .darkMode{
        background-color: hsl(207, 26%, 17%);
        .boardOutter{
            background-color: hsl(209, 23%, 22%);
            color: hsl(0, 0%, 98%);;
        }
    }
    .lightMode{
        background-color: hsl(0, 0%, 98%);
        .boardOutter{
            width: 80%;
            margin: 0 auto 40px;
            background-color:  hsl(0, 0%, 100%);
            color: hsl(200, 15%, 8%);
            border: 1px solid  hsl(0, 0%, 98%);
            border-radius: 5px;
        }
    }
    .list{
        min-height: calc(100vh - 174px); 
        display: flex;
        flex-wrap: wrap;
        padding: 0 60px;
        /deep/ .van-image{
            width: 300px;
            height: 13vw;
        }
        .boardOutter{
            width: 300px;
            margin: 0 auto;
            margin-bottom: 60px;
            padding-bottom: 30px;
            .text{
                div{
                    text-align: left;
                    padding-left: 20px;
                }
                .name{
                    height: 40px;
                    line-height: 40px;
                    font-size: 18px;
                }
                .textTitle{
                    height: 20px;
                    line-height: 20px;
                    font-size: 14px; 
                }
            }
        }
    }
}
</style>