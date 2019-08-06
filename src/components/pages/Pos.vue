<template>
    <div>
        <el-row>
            <el-col :span="7" class="pos-order" id="order-list">
                <el-tabs>
                    <el-tab-pane label="点餐">
                        <el-table :data="tableData" broder style="width:100%">
                            <el-table-column prop="goodsName" label="商品"></el-table-column>
                            <el-table-column prop="count" label="数量"></el-table-column>
                            <el-table-column prop="price" label="金额"></el-table-column>
                            <el-table-column  label="操作" fixed="right">
                                <template >
                                    <div>
                                        <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                                        <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                                    </div>

                                </template>
                            </el-table-column>
                        </el-table>
                        <div class="totalDiv"> 数量：{{totalCount}} &nbsp;&nbsp;&nbsp;&nbsp; 金额:{{totalMoney}}</div>
                        <div class="but1">
                            <el-button type="warning" class="button">挂单</el-button>
                            <el-button type="success" class="button" @click="checkout()">结账</el-button>
                            <el-button type="danger" class="button" @click="delAllGoods()">删除</el-button>
                        </div>

                    </el-tab-pane>
                    <el-tab-pane label="挂单"></el-tab-pane>
                    <el-tab-pane label="外卖"></el-tab-pane>
                </el-tabs>
            </el-col>
            <el-col :span="15">
                <div class="often-goods">
                    <div class="title">常用商品</div>
                    <div class="often-goods-list">
                        <ul>
                            <li v-for="item of oftenGoods" :key="item.goodsId" @click="addOrderList(item)">
                                <span>{{item.goodsName}}</span>
                                <span class="goods-price">{{item.price}}</span>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="goods-type">
                    <el-tabs class="menu">
                        <el-tab-pane label="汉堡">
                            <ul class='cookList'>
                                <li v-for=" item of type0Goods" :key="item.goodsId" @click="addOrderList(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">{{item.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                        <el-tab-pane label="小食">
                            <ul class='cookList'>
                                <li v-for=" item of type1Goods" :key="item.goodsId" @click="addOrderList(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">{{item.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                        <el-tab-pane label="饮料">
                            <ul class='cookList'>
                                <li v-for=" item of type2Goods" :key="item.goodsId" @click="addOrderList(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">{{item.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                        <el-tab-pane label="套餐">
                            <ul class='cookList'>
                                <li v-for=" item of type3Goods" :key="item.goodsId" @click="addOrderList(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">{{item.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                    </el-tabs>
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Pos',
    created(){

        axios.get('http://old.jspag.com/DemoApi/oftenGoods.php')
        .then(response=>{
            console.log(response);
            this.oftenGoods=response.data;
        })
        .catch(error=>{
            console.log(error);
            alert('网络错误，不能访问');
        })
        axios.get('http://jspang.com/DemoApi/typeGoods.php')
        .then(response=>{
            console.log(response);
            //this.oftenGoods=response.data;
            this.type0Goods=response.data[0];
            this.type1Goods=response.data[1];
            this.type2Goods=response.data[2];
            this.type3Goods=response.data[3];
 
      })
        .catch(error=>{
            console.log(error);
            alert('网络错误，不能访问');
        })
  },
    mounted(){
        var orderHeight=document.body.clientHeight
        document.getElementById('order-list').style.height=orderHeight + 'px'
    },
    data() {
        return{

            tableData: [{
          goodsName: '可口可乐',
          price: 8,
          count:1
        }, {
          
          goodsName: '香辣鸡腿堡',
          price: 15,
          count:1
        }, {
         
          goodsName: '爱心薯条',
          price: 8,
          count:1
        }, {
         
          goodsName: '甜筒',
          price: 8,
          count:1
        }],
        oftenGoods:[],
        type0Goods:[],
        type1Goods:[],
        type2Goods:[],
        type3Goods:[],
        totalMoney: 0,
        totalCount: 0
        }
    },
    methods:{
        checkout() {
            if (this.totalCount!=0) {
                this.tableData = [];
                this.totalCount = 0;
                this.totalMoney = 0;
                this.$message({
                    message: '结账成功，感谢你又为店里出了一份力!',
                    type: 'success'
                });
        
            }else{
                this.$message.error('不能空结。老板了解你急切的心情！');
            }
        
        },
        delAllGoods() {
            this.tableData = [];
            this.totalCount = 0;
            this.totalMoney = 0;
            },
     //添加订单列表的方法
        addOrderList(goods){
            this.totalCount=0; //汇总数量清0
            this.totalMoney=0;
            let isHave=false;
            //判断是否这个商品已经存在于订单列表
            for (let i=0; i<this.tableData.length;i++){
                console.log(this.tableData[i].goodsId);
                if(this.tableData[i].goodsId==goods.goodsId){
                    isHave=true; //存在
                }
            }
            //根据isHave的值判断订单列表中是否已经有此商品
            if(isHave){
                //存在就进行数量添加
                let arr = this.tableData.filter(o =>o.goodsId == goods.goodsId);
                arr[0].count++;
                //console.log(arr);
            }else{
                //不存在就推入数组
                let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                this.tableData.push(newGoods);
            }
            this.getAllMoney();
            //进行数量和价格的汇总计算
            this.tableData.forEach((element) => {
                this.totalCount+=element.count;
                this.totalMoney=this.totalMoney+(element.price*element.count);   
            });
    
},
        delSingleGoods(goods){
            console.log(goods);
            this.tableData=this.tableData.filter(o => o.goodsId !=goods.goodsId);
            this.getAllMoney();
    
      },
      //汇总数量和金额
        getAllMoney(){
            this.totalCount=0;
            this.totalMoney=0;
            if(this.tableData){
                    this.tableData.forEach((element) => {
                this.totalCount+=element.count;
                this.totalMoney=this.totalMoney+(element.price*element.count);   
            });
            }    
        } 
        }
}
</script>

<style  scoped>
.pos-order{
    background: #F9FAFC;
    border-right: 1px solid #C0CCDA; 
}
.button{
    margin-top: 10px;
    display: inline-block
}
.but1{
    text-align: center;
}
.goods-price{
    color: #58B7FF;
}
.title{
       height: 20px;
       border-bottom:1px solid #D3DCE6;
       background-color: #F9FAFC;
       padding:10px;
       margin: 0 auto;
   }
.often-goods-list ul li{
    list-style: none;
    float:left;
    border:1px solid #E5E9F2;
    padding:10px;
    margin:5px;
    background-color:#fff;
} 
.goods-type{
    clear: both;
}
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
 
   }
.cookList li span{
    
    display: block;
    float:left;
}
.foodImg{
    width: 40%;
}
.foodName{
    font-size: 18px;
    padding-left: 10px;
    color:brown;

}
.foodPrice{
    font-size: 16px;
    padding-left: 10px;
    padding-top:10px;
}
.totalDiv{
    background: #fff;
    overflow: hidden;
    border-bottom: 1px solid #D3DCE6
}

</style>