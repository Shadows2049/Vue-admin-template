<template>
  <div class="login-container">
    <el-row>
      <el-col :span="19">
        <particles />
        <transition
          appear
          name="animate__animated animate__slideInDown animate__slow 3s"
          enter-active-class="animate__slideInDown"
        >
          <div class="ds">
            <el-card class="box-card">
              <el-form
                ref="loginForm"
                :model="loginForm"
                :rules="loginRules"
                class="login-form"
                auto-complete="on"
                label-position="left"
                style="border-radius: 30px"
              >
                <div class="title-container">
                  <h3 class="title">Login Form</h3>
                </div>

                <el-form-item prop="username">
                  <span class="svg-container">
                    <svg-icon icon-class="user" />
                  </span>
                  <el-input
                    ref="username"
                    v-model="loginForm.username"
                    placeholder="Username"
                    name="username"
                    type="text"
                    tabindex="1"
                    auto-complete="on"
                    clearable="true"
                  />
                </el-form-item>

                <el-form-item prop="password">
                  <span class="svg-container">
                    <svg-icon icon-class="password" />
                  </span>
                  <el-input
                    :key="passwordType"
                    ref="password"
                    v-model="loginForm.password"
                    :type="passwordType"
                    placeholder="Password"
                    name="password"
                    tabindex="2"
                    auto-complete="on"
                    @keyup.enter.native="handleLogin"
                    clearable="true"
                  />
                  <transition
                    appear
                    name="animate__animated animate__flash animate__delay-2s animate__slow 5s"
                    enter-active-class="animate__flash"
                  >
                    <span class="show-pwd" @click="showPwd">
                      <svg-icon
                        :icon-class="
                          passwordType === 'password' ? 'eye' : 'eye-open'
                        "
                      />
                    </span>
                  </transition>
                </el-form-item>

                <el-button
                  :loading="loading"
                  type="primary"
                  style="
                    width: 100%;
                    margin-bottom: 30px;
                    -webkit-filter: drop-shadow(1px 2px 22px rgb(54, 152, 245));
                  "
                  @click.native.prevent="handleLogin"
                  >Login</el-button
                >

                <div class="tips">
                  <span
                    style="
                      margin-right: 20px;
                      -webkit-filter: drop-shadow(
                        1px 2px 5px rgb(238, 218, 128)
                      );
                    "
                    >username: admin</span
                  >
                  <span
                    style="
                      -webkit-filter: drop-shadow(
                        1px 2px 5px rgb(238, 218, 128)
                      );
                    "
                  >
                    password: any</span
                  >
                </div>
              </el-form>
            </el-card>
          </div>
        </transition>
      </el-col>

      <el-col :span="5">
        <transition
          appear
          name="animate__animated animate__fadeInRight animate__slow 3s"
          enter-active-class="animate__fadeInRight"
        >
          <el-card class="box-card2"></el-card>
        </transition>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { validUsername } from '@/utils/validate'

import particles from '@/components/Particles/particles.vue'
export default {
  name: 'Login',
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!validUsername(value)) {
        callback(new Error('Please enter the correct user name'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('The password can not be less than 6 digits'))
      } else {
        callback()
      }
    }
    return {
      color1: 'fff',
      loginForm: {
        username: 'admin',
        password: '111111'
      },
      loginRules: {
        username: [
          { required: true, trigger: 'blur', validator: validateUsername }
        ],
        password: [
          { required: true, trigger: 'blur', validator: validatePassword }
        ]
      },
      loading: false,
      passwordType: 'password',
      redirect: undefined
    }
  },
  watch: {
    $route: {
      handler: function (route) {
        this.redirect = route.query && route.query.redirect
      },
      immediate: true
    }
  },
  methods: {
    showPwd() {
      if (this.passwordType === 'password') {
        this.passwordType = ''
      } else {
        this.passwordType = 'password'
      }
      this.$nextTick(() => {
        this.$refs.password.focus()
      })
    },
    handleLogin() {
      this.$refs.loginForm.validate((valid) => {
        if (valid) {
          this.loading = true
          this.$store
            .dispatch('user/login', this.loginForm)
            .then(() => {
              this.$router.push({ path: this.redirect || '/' })
              this.loading = false
            })
            .catch(() => {
              this.loading = false
            })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  },
  components: { particles }
}
</script>

<style lang="scss">
/* 修复input 背景不协调 和光标变色 */
/* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

$bg: #283443;
$light_gray: #fff;
$cursor: #fff;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container .el-input input {
    color: $cursor;
  }
}

/* reset element-ui css */

.el-input {
  display: inline-block;
  height: 47px;
  width: 85%;

  input {
    background: transparent;
    border: 0px;
    -webkit-appearance: none;
    -webkit-filter: drop-shadow(1px 2px 15px rgb(255, 212, 22));
    border-radius: 0px;

    padding: 12px 5px 12px 15px;
    color: $light_gray;

    caret-color: $cursor;
    &:-webkit-autofill {
      box-shadow: 0 0 0px 1000px $bg inset !important;
      -webkit-text-fill-color: $cursor !important;
    }
  }
}

.el-form-item {
  border: 2px solid rgba(101, 163, 255, 0.911);
  border-bottom: 6px solid rgba(101, 163, 255, 0.911);
  background: rgba(0, 217, 255, 0.034);
  border-radius: 6px;
  color: #454545;
}
</style>

<style lang="scss" scoped>
$bg: #173c52;
$bg2: rgb(255, 255, 255);
$dark_gray: #889aa4;
$light_gray: #eee;

.login-container {
  min-height: 100%;
  min-width: 600px;
  width: 100%;
  background-color: $bg;
  overflow: auto;

  .box-card {
    z-index: 5;

    background-color: transparentize($color: rgb(56, 53, 221), $amount: 0.88);
    -webkit-clip-path: polygon(
      75% 0,
      100% 27%,
      100% 100%,
      50% 100%,
      0 100%,
      0 0
    );

    margin: 10% auto;

    min-width: 100%;
    height: 100%;
    overflow: auto;
    border-width: 2px;
    border-color: #41d1eb;
    border-right: 120px solid transparent;

    border-bottom: 20px solid #41d1eb;
    box-shadow: 15px 15px 300px rgba(63, 111, 182, 0.527);
  }

  .box-card2 {
    background-color: transparentize($color: rgb(56, 53, 221), $amount: 0.88);

    margin: 0 auto;

    min-width: 100%;
    height: 100vh;
    min-height: 500px;
    min-width: 300px;
    overflow: auto;
    border-width: 2px;
    border-color: #41d1eb;
    border-left: 120px solid transparent;
    border-top: 20px solid #41d1eb;
    border-bottom: 20px solid #41d1eb;
    -webkit-filter: drop-shadow(50px 10px 20px #0ec8e9);
  }

  .ds {
    -webkit-filter: drop-shadow(0px 15px 35px #0ec8e9);
  }

  .login-form {
    position: relative;
    width: 100%;
    max-width: 520px;
    padding: 90px 35px;
    margin: 0 auto;
    overflow: auto;
  }

  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;

    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }

  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
  }

  .title-container {
    position: relative;

    .title {
      font-size: 26px;
      color: $light_gray;
      margin: 0px auto 40px auto;
      text-align: center;
      font-weight: bold;
    }
  }

  .show-pwd {
    position: absolute;
    top: 7px;
    font-size: 16px;
    color: #fff;
    cursor: pointer;
    user-select: none;
    -webkit-filter: drop-shadow(0px 4px 3px rgb(11, 132, 180));
  }
}

.el-carousel__item h3 {
  color: #475669;
  font-size: 14px;
  opacity: 0.75;
  line-height: 200px;
  margin: 0;
}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}
</style>
