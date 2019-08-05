<template>
    <div>
        <el-row>
            <el-col :span="10" class="pos-order" id="order-list">
                我是订单
            </el-col>
            <el-col :span="10">
                我是产品
            </el-col>
        </el-row>
    </div>
</template>

<script>
export default {
    name: 'Pos',
    mounted(){
        var orderHeight=document.body.clientHeight
        document.getElementById('order-list').style.height=orderHeight + 'px'
    }
}
</script>

<style  scoped>
.pos-order{
    background: #F9FAFC;
    border-right: 1px solid #C0CCDA; 
}   
</style>