<template>
    <div>
        <ul>
            <li v-for="good in goods" v-bind:key="good.id">
                <b>
                <p>good name: {{good.goodName}}</p>
                <p>good price: {{good.goodPrice}}</p>
                <p>good detail: {{good.goodDetail}}</p>
                <p>repository count: {{good.repoCount}}</p>
                <button v-on:click="rush(good.id)">RUSH</button></b>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "Index.vue",
        data: function () {
            return {
                goods: []
            }
        },
        methods: {
            getGoods: function () {
                //向后台获取商品信息
                this.axios.get("/api/main/good").then((response)=>{
                    //将所得数据赋值给goods属性，response代表响应对象，其中的data属性代表响应体中的内容
                    this.goods = response.data;
                })
            },
            rush: function(goodId) {
                //提交抢购的请求
                this.axios.post("/api/rush/",
                    {
                        goodId:goodId,
                        userId:this.$store.getters.getUser.id,
                        amount:1,
                        status:0
                    }).then((response)=>{
                        alert(response.data);
                        //刷新商品数据
                        this.getGoods()
                })
            }
        },
        created: function () {
            //在页面创建时，调用查询商品的方法
            this.getGoods();
        }
    }
</script>

<style scoped>
    div {
        font-family: "Ink Free";
        font-size: 18px;
        color: cornflowerblue;
        background: url("../assets/dio.jpg");
        background-size: auto;
    }
    ul {
        list-style-type: none;
    }
    li{
        border-bottom: 1px solid black;
    }
    button {
        background-color: #4CAF50;
        color: white;
        padding: 14px 20px;
        margin: 8px 0;
        border: none;
        cursor: pointer;
    }

    button:hover {
        opacity: 0.8;
    }
</style>