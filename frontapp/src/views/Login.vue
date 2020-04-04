<template>
    <div class = "container">
        <img src = "../assets/bilibili.png" width="330px" height="155px">
        <b>
        <h1 style = "font-size: 40px">E-Commerce Platform</h1>
        <div class = "input-box">
            <label>Username</label>
            <input type = "text" v-model = "user.username"/>
            <!--v-model实现的是双向绑定，也就是value的值改变会带动user.username的改变，反之一样-->
        </div>
        <div class = "input-box">
            <label>Password</label>
            <input type = "password" v-model = "user.password"/>
        </div>
        <div class = "input-box">
            <button v-on:click = "login">Submit</button>
            <button v-on:click = "clear">Clear</button>
        </div>
        </b>
    </div>

</template>

<script>
    //ctrl + alt + l Quick formatting code
    export default {
        name: "Login",
        data: function(){
            return {
                user: {
                    username: "chenyimin",
                    password: "123456"
                }
            }
        },
        methods: {
            clear () {
                /* ctrl + / 快速注释， ctrl + shift + / 快速块状注释*/
            //    清空输入框中的内容，data中的任意属性都可以通过this对象获取，this代表的是当前的页面实例对象
                this.user.username = "";
                this.user.password = "";
            },
            login () {
                //通过获取axios对象，调用其post方法发送http请求
                //post第一个参数是地址，第二个参数是要提交的数据
                this.axios.post("/api/main/login", this.user).then((response)=>{
                    //将后台获取到的userInfo保存至前台的浏览器缓存中，resp代表response，resp.data代表获取到的用户信息
                    //通过获取vuex的store对象，调用其commit方法存储从后台获取到的user对象
                    this.$store.commit("setUser", response.data);

                    //进入详情页，实际上是让router的路径指向/index
                    this.$router.push({path:"/index"});
                })
            }
        }
    }
</script>

<style scoped>
    label {
        width:80px;
        display:inline-block;
    }
    .input-box {
        margin-bottom:20px;
    }
    .container {
        height: 780px;
        font-family: "Ink Free";
        font-stretch: normal;
        color: mediumpurple;
        background: url("../assets/kazi.jpg");
        background-size: auto;
    }
    button {
        margin-right:10px;
        background-color: mediumpurple;
        color: white;
        padding: 14px 20px;
        border: none;
        cursor: pointer;
    }

    button:hover {
        opacity: 0.8;
    }
</style>