<template>
    <div id="login">
        <div class="login-wrapper">
            <div class="login-container">
                <div class="login-brand">
                    <img src="~@/assets/img/logo.png">
                </div>
                <div class="login-box">
                    <el-form class="login-form" :model="form" @submit.native.prevent="verify" label-position="top">
                        <el-form-item class="tip">系统登录</el-form-item>
                        <el-form-item label="用户名">
                            <el-input v-model="form.username" auto-complete='off' />
                        </el-form-item>
                        <el-form-item label="密码">
                            <el-input v-model="form.password" auto-complete='off' type="password" show-password />
                        </el-form-item>
                        <el-form-item label=" ">
                            <el-input class="submit" type="submit" value="登录" />
                        </el-form-item>
                    </el-form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'login',
    data() {
        return {
            form: {
                username: 'admin',
                password: '123456'
            }
        }
    },
    methods: {
        verify() {
            let usernameMsg = '请输入用户名'
            let passwordMsg = '请输入密码'
            if (!this.form.username) {
                this.$message.error(usernameMsg)
            } else if (!this.form.password) {
                this.$message.error(passwordMsg)
            } else {
                this.login()
            }
        },
        login() {
            let successMsg = '登录成功'
            let errorMsg = '账号或密码错误'
            this.$store.dispatch('GET_LOGIN_DATA', this.form).then((res) => {
                this.$message.success(successMsg)
                this.$route.query.redirect ? this.$router.push(this.$route.query.redirect) : this.$router.push('/')
            }).catch((err) => {
                console.log(err)
                this.$message.error(errorMsg)
            })
        }
    }
}
</script>
<style lang='stylus'>
$loginPrimary = #304352;
$loginPrimaryRGB = 48,67,82;
$loginGrey = rgba($loginPrimaryRGB, 0.06);
$loginDark = rgba($loginPrimaryRGB, 0.5);
#login {
    position: relative;
    width: 100%;
    min-height: 100vh;
    background: rgba($loginPrimary, 0.4);
    background-image: linear-gradient(to bottom, #d7d2cc 0%, #304352 100%);
    .login-wrapper {
        width: 360px;
        padding: 150px 0;
        margin: 0 auto;
        .login-container {
            position: relative;
            .login-brand {
                position: relative;
                width: 100px;
                height: 100px;
                margin: 0 auto -50px auto;
                border-radius: 50%;
                box-shadow: 0 4px 40px rgba(0, 0, 0, 0.07);
                padding: 10px;
                background-color: #fff;
                z-index: 1;
                overflow: hidden;
                img {
                    width: 100%;
                }
            }
            .login-box {
                position: relative;
                width: 100%;
                height: 100%;
                background-color: #fff;
                box-shadow: 0 7px 25px rgba(0, 0, 0, 0.08);
                padding: 60px 25px 25px 25px;
                border-radius: 3px;
                .login-form {
                    .tip {
                        color: $loginDark;
                        text-align: center;
                        font-weight: 700;
                        margin-top: 10px;
                    }
                    .el-form-item__label {
                        color: $loginDark;
                        font-weight: 700;
                        padding: 0;
                    }
                    .el-input__inner {
                        height: 45px;
                        line-height: 45px;
                        background: $loginGrey;
                        border: none;
                    }
                    .submit {
                        cursor: pointer;
                        input {
                            width: 100%;
                            color: #fff;
                            border-radius: 3px;
                            background-color: $loginPrimary;
                            box-shadow: 0 2px 7px $loginDark;
                            font-weight: 700;
                            cursor: pointer;
                            border: none;
                            outline: 0;
                            transition: all 0.3s;
                        }
                        &:hover {
                            input {
                                opacity: 0.8;
                            }
                        }
                    }
                }
            }
            &:after {
                content: ' ';
                position: absolute;
                top: 100%;
                left: 50%;
                width: 88%;
                height: 5px;
                transform: translateX(-50%);
                background-color: #f0f0f0;
                border-radius: 0 0 3px 3px;
            }
        }
    }
}
</style>
