<template>
    <div class="app">
        <div class="Notice">
            <div id="title">登录:</div>
            <div id="text">请输入用户名和密码:</div>
        </div>
        <div class="Inputs">
            <div class="Userid">
                用户名:
                <input v-model="Userid" onkeyup="value=value.replace(/[^\w\.\/]/ig,'')" />
            </div>
            <div class="Password">
                密码:
                <input
                    v-model="Password"
                    type="password"
                    onkeyup="value=value.replace(/[^\w\.\/]/ig,'')"
                />
            </div>
            <div id="Submit" @click="Login()">登录</div>
        </div>
    </div>
</template>
<style lang="scss">
template {
    font-family: "微软雅黑";
}
#title {
    font-size: 40px;
    font-weight: bold;
}
#text {
    font-size: 25px;
    text-align: left;
    height:40px;
    margin: 0 auto;
    width: 500px;
}
.Inputs {
    display: flex;
    flex-direction: column;
    font-size: 25px;
    gap: 5px;
    width: 500px;
    text-align: center;
    margin: 0 auto;
}
.Inputs input {
    font-size: 25px;
}
.Inputs > div {
    width: 100%;
    text-align: left;
}
#Submit {
    font-size: 30px;
    width: 80px;
    height: 50px;
    line-height: 50px;
    text-align: center;
    background-color: #6cf;
    border-radius: 20%;
    margin: 0 auto;
    user-select: none;
}
#Submit:hover {
    cursor: pointer;
    box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
        0 17px 50px 0 rgba(0, 0, 0, 0.19);
}
</style>

<script>
import axios from 'axios'
export default ({
    name: 'register',
    data() {
        return {
            Userid: '',
            Password: '',
        }
    },
    methods:{
        Login()
        {
            axios({
            method: 'post',
            url: 'http://127.0.0.1:8000/auth/login',
            data: {
                "username": this.Userid,
                "password": this.Password,
                }
            });
        }
    }
})
</script>