<template>
  <div class="operOutter " :class='isDark ? "operLightMode" : "operDarkMode"'>
    <div class="left">
        <van-search
            @search="onSearch"
            v-model="value"
            placeholder="Seach for a country..."
        />
    </div>
    <div class="right">
        <van-popover
            v-model="showPopover"
            trigger="click"
            :actions="actions"
            @select="onSelect"
            theme="dark"
        >
        <template #reference>
            <van-button size="small" icon="arrow-down" icon-position="right">
                Filter by Region
            </van-button>
        </template>
        </van-popover>
       
    </div>
  </div>
</template>

<script>
import Search from 'vant/lib/search';
import Popover from 'vant/lib/popover';
import Button from 'vant/lib/button';
import 'vant/lib/popover/style';
import 'vant/lib/button/style';
import 'vant/lib/search/style';


export default {
    components: {
        [Search.name]: Search,
        [Button.name]: Button,
        [Popover.name]: Popover
    },
    props: ['isDark'],
    data () {
        return {
            showPopover: false,
            value: '',
            actions: [{ text: 'Africa' }, { text: 'Americas' },{ text: 'Asia' }, { text: 'Europe' }, { text: 'Oceania' }],
        }
    },
    methods: {
        onSearch (val) {
            this.$emit('setSearch', val)
        },
        onSelect(actions) {
            this.$emit('setScreening', actions.text)
        }
    }
}
</script>

<style lang="less" scoped>
.operDarkMode{
    padding: 35px 0;
    /deep/ .van-field__left-icon{
        color: hsl(0, 0%, 100%);
    }
  
}
.operLightMode{
    padding: 35px 0;
    /deep/ .van-field__left-icon{
        color: hsl(200, 15%, 8%);
    }
  
}
/deep/ .van-popover--light {
    .van-popover__content{
        background-color:hsl(209, 23%, 22%);
    }
}
@media screen and (max-width: 376px) {
    .operDarkMode{
        background-color:hsl(207, 26%, 17%);
        /deep/ .van-search__content{
        background-color: hsl(209, 23%, 22%);
            .van-field__control{
                color: hsl(0, 0%, 100%);
            }    
        }
        /deep/ .van-button--default {
            color: hsl(0, 0%, 100%);
            background-color:hsl(209, 23%, 22%);
            border: 1px solid hsl(207, 26%, 17%);
        }
        /deep/ .van-search{
            background-color: hsl(207, 26%, 17%);
        }
    }
    .operLightMode{
        background-color: hsl(0, 0%, 98%);
        /deep/ .van-search__content{
            background-color: hsl(0, 0%, 100%);
            .van-field__control{
                color: hsl(0, 0%, 52%);
            }    
        }
        /deep/ .van-button--default {
            color:hsl(200, 15%, 8%);
            background-color:hsl(0, 0%, 100%);
            border: 1px solid hsl(0, 0%, 98%);
        }
        /deep/ .van-search{
            background-color: hsl(0, 0%, 98%);
        }
    }
    
    .operOutter{
        .right{
            text-align: left;
            padding-left: 10px;
        }
    }
}
@media screen and (min-width: 1440px) {
    .operDarkMode{
        background-color: hsl(207, 26%, 17%);
        /deep/ .van-button--default {
            color: hsl(0, 0%, 100%);
            background-color: hsl(209, 23%, 22%);
            border: 1px solid hsl(207, 26%, 17%);
        }   
        /deep/ .van-search{
            background-color: hsl(207, 26%, 17%);
        }
        /deep/ .van-search__content{
            background-color: hsl(209, 23%, 22%);
        }
        .van-field__control{
            color: hsl(0, 0%, 100%);
        } 
    }
    .operLightMode{
        background-color:  hsl(0, 0%, 98%);
        /deep/ .van-button--default {
            color:  hsl(200, 15%, 8%);
            background-color: hsl(0, 0%, 100%);
            border: 1px solid hsl(0, 0%, 98%);
        }   
        /deep/ .van-search{
            background-color: hsl(0, 0%, 100%);
        }
        /deep/ .van-search__content{
            background-color: hsl(0, 0%, 100%);
        }
        .van-field__control{
            color: hsl(0, 0%, 52%);
        } 
    }
     
    /deep/ .van-search{
        width: 300px;
        padding: 0;
        
    }
    .operOutter{
        display: flex;
        div{
            flex: 1;
        }
    }
    .operOutter{
        .left{
            text-align: left;
            padding-left: 60px;
        }
        .right{
            text-align: right;
            padding-right: 60px;
        }
    }
}

</style>