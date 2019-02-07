<template>
    <div>
        <form v-if="!isReg">
            <div>
                <label name="userName">用户名：</label>
                <input type="text" name="userName" v-model="userName">
            </div>
            <div>
                <label name="passWord">密码：</label>
                <input type="password" name="passWord" v-model="passWord">
            </div>
            <button type="button" @click="login()">登录</button>
            <button type="button" @click="reg()">注册</button>
        </form>
        <form v-else>
            <div>
                <label name="userName">用户名：</label>
                <input type="text" name="userName" v-model="userName">
            </div>
            <div>
                <label name="passWord">密码：</label>
                <input type="password" name="passWord" v-model="passWord">
            </div>
            <div>
                <label name="repeat">再次输入密码：</label>
                <input type="password" name="repeat" v-model="repeat">
            </div>
            <button type="button" @click="addUser()">确定</button>
            <button type="button" @click="cancel()">取消</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: "Login",
        data() {
            return {
                isReg: false,
                userName: '',
                passWord: '',
                repeat: '',
            }
        },

        methods: {
            login() {
                if (localStorage.getItem("userName") === this.userName && localStorage.getItem("passWord") === this.passWord)
                {
                    this.userName='';
                    this.passWord='';
                    this.$router.push('/home')
                }else {
                    alert("您输入的账户或者密码不正确")
                }
            },
            reg() {
                this.isReg = true
            },
            cancel() {
                this.isReg = false
            },
            addUser() {
                if (this.passWord === '' || this.repeat === '') {
                    alert("密码不能为空")
                }
                if (this.passWord == this.repeat) {
                    localStorage.setItem("userName", this.userName);
                    localStorage.setItem("passWord", this.passWord);
                    this.userName = '';
                    this.passWord = '';
                    this.isReg = true
                } else {
                    alert("两次密码输入不正确")
                }

            }
        }
    }
</script>

<style scoped>

</style>
