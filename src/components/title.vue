<template>
  <div :class='isDark ? "lightMode" : "titleDarkMode"' class="titleOutter">
      <div class="left">Where in the world?</div>
      <div class="right" @click="isDark = !isDark">Dark Mode</div>
  </div>
</template>

<script>
export default {
    data () {
        return {
            isDark: false
        }
    },
    created () {
        this.isDark = sessionStorage.getItem('isDark')
    },
    watch: {
        'isDark': {
            handler (newV) {
                sessionStorage.setItem('isDark', newV) 
                this.$emit('setMode', newV)
            }
        }
    }
}
</script>

<style lang="less" scoped>
.titleDarkMode{
    background-color: hsl(209, 23%, 22%);
    color: hsl(0, 0%, 100%);
}
.lightMode{
    background-color:  hsl(0, 0%, 98%);
    color: hsl(200, 15%, 8%);
}
@media screen and (min-width: 1440px) {
    .titleOutter{
        height: 70px;
        line-height: 70px;
        width: 100%;
        display: flex;
        div{
            flex: 1;
        }
        .left{
            text-align: left;
            padding-left: 60px;
            font-size: 16px;
            font-weight: 600;
        }
        .right{
            text-align: right;
            padding-right: 60px;
            font-size: 14px;
        }
    }
}
@media screen and (max-width: 376px){
    //手机样式
    .titleOutter{
        height: 70px;
        line-height: 70px;
        width: 100%;
        display: flex;
    }
    div{
        flex: 1;
    }
    .left{
        text-align: left;
        padding-left: 30px;
        font-size: 16px;
        font-weight: 600;
    }
    .right{
        text-align: right;
        padding-right: 30px;
        font-size: 14px;
    }
}

</style>