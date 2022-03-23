<template>
    <div class="app">
        <div class="Notice">
            <div id="title">注册须知:</div>
            <ul>
                <li>用户名仅限字母和数字,不超过8个字符</li>
                <li>需绑定一个可用邮箱</li>
                <li>密码需包含字母和数字,不少于8个字符</li>
            </ul>
        </div>
        <div class="Inputs">
            <div class="Userid">
                用户名:
                <input v-model="Userid" onkeyup="value=value.replace(/[^\w\.\/]/ig,'')" />
            </div>
            <div class="EmailAddress">
                邮箱:
                <input v-model="EmailAddress" />
            </div>
            <div class="Password">
                密码:
                <input
                    v-model="Password"
                    type="password"
                    onkeyup="value=value.replace(/[^\w\.\/]/ig,'')"
                />
            </div>
            <div class="PasswordRepeat">
                确认密码:
                <input
                    v-model="PasswordRepeat"
                    type="password"
                    onkeyup="value=value.replace(/[^\w\.\/]/ig,'')"
                />
            </div>
            <div id="Submit" @click="Register()">注册</div>
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
.Notice > ul {
    font-size: 25px;
    list-style-type: disc;
    list-style-position: inside;
    text-align: left;
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
            EmailAddress: '',
            Password: '',
            PasswordRepeat: '',
        }
    },
    methods: {
        Check_Password() {
            if (this.Password.length < 8 || this.PasswordRepeat.length < 8 || this.Password !== this.PasswordRepeat) return 0;
            let flag_alpha = 0;
            let flag_num = 0;
            for (let idx = 0; idx < this.Password.length; idx++) {
                if (this.Password[idx] >= "0" && this.Password[idx] <= "9") flag_num = 1;
                if (this.Password[idx] >= "a" && this.Password[idx] <= "z") flag_alpha = 1;
                if (this.Password[idx] >= "A" && this.Password[idx] <= "Z") flag_alpha = 1;
            }
            return (flag_alpha && flag_num);
        },
        Check_Email() {
            let tst = /@/;
            if (!tst.test(this.EmailAddress)) return 0;
            tst = /./;
            if (!tst.test(this.EmailAddress)) return 0;
            tst = / /;
            if (tst.test(this.EmailAddress)) return 0;
            return 1;
        },
        Check_is_Possible() {
            if (this.Userid.length >= 8) {
                this.Userid = '';
                alert("用户名输入不合法,请重新输入");
                return;
            }
            if (!this.Check_Email()) {
                this.EmailAddress = '';
                alert("邮箱输入不合法,请重新输入");
                return;
            }
            if (!this.Check_Password()) {
                this.Password = '';
                this.PasswordRepeat = '';
                alert("密码不合法或两次密码不一致,请重新输入");
                return;
            }
            alert("用户注册成功")
        },
        Register()
        {
            this.Check_is_Possible();
            axios({
            method: 'post',
            url: 'http://127.0.0.1:8000/auth/register',
            data: {
                "email": this.EmailAddress,
                "username": this.Userid,
                "password": this.Password,
                }
            });
        }
        
    }
})
</script>
