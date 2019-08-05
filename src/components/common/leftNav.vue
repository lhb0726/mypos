<template>
    <div class="left-nav"> 
        <ul>
            <li>
                <i class="icon iconfont icon-goumai"></i>
                <div>购买</div>
            </li>
            <li>
                <i class="icon iconfont icon-dianpu"></i>
                <div>店铺</div>
            </li>
            <li>
                <i class="icon iconfont icon-hanbao"></i>
                <div>商品</div>
            </li>
            <li>
                <i class="icon iconfont icon-VIP"></i>
                <div>会员</div>
            </li>
            <li>
                <i class="icon iconfont icon-gongnengjianyi"></i>
                <div>统计</div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'leftNav'
}
</script >


<style >
.left-nav{
    color: #fff;
    height: 100%;
    font-size: 10px;
    float: left;
    width: 5%;
    background: #1D8CE0;
}
.iconfont{
    font-size: 20px;
    margin: 0 auto
} 
.left-nav ul{
    padding: 0;
    margin: 0;
}
.left-nav li{
    list-style: none;
    border-bottom: 1px solid #20a0ff;
    padding: 10px;
    text-align: center
}
</style>