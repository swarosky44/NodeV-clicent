<template>
  <div class="g-lock"></div>
  <div v-else class="m-box">
    <p class="u-login-tit">请认真填写以下信息，O(∩_∩)O</p>
    <div class="m-item f-mr-t">
      <i></i>
      <input class="u-item" :class="{'error-tip': statusName}" v-model="username" type="text" @change="confirmName" placeholder="请输入账号">
    </div>
    <div class="m-item">
      <i></i>
      <input class="u-item" :class="{'error-tip': statusPwd}" v-model="pwd" type="password" @change="confirmPwd"placeholder="请输入密码">
    </div>
    <div class="m-item">
      <i></i>
      <input class="u-item" :class="{'error-tip': statusPwdr}" v-model="pwdr" type="password" @change="confirmPwdr" placeholder="请再次输入密码">
    </div>
    <div class="m-btns2">
      <button class="u-commit" @click="commit">提交</button>
    </div>
    <a class="m-leave" href="javascript:;" @click="cancel"> >>> Leave Here</a>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        username: '',
        pwd: '',
        pwdr: '',
        statusPwdr: false,
        statusPwd: false,
        statusName: false
      }
    },
    methods: {
      cancel () {
        let opt = {
          status: false
        }
        this.$dispatch('rWindow', opt)
      },
      commit () {
        let user = {
          username: this.username,
          pwd: this.pwd
        }
        if (!this.username) {
          this.statusName = true
          return
        }
        if (!this.pwd) {
          this.statusPwd = true
          return
        }
        if (!this.pwdr) {
          this.statusPwdr = true
          return
        }
        this
        .$http.post('api/regis', user)
        .then((res) => {
          console.log(res.data.err)
          if (res.data.err === 0) {
            this.$parent.rStatus = false
            this.$parent.status = false
            return
          }
          if (res.data.err === 2) {
            this.statusName = true
            return
          }
        },
        (err) => {
          console.log(err)
        })
      },
      confirmPwdr () {
        if (this.pwd === this.pwdr || this.pwdr) {
          this.statusPwdr = false
        } else {
          this.statusPwdr = true
        }
      },
      confirmPwd () {
        if (this.pwd === this.pwdr || this.pwd) {
          this.statusPwd = false
        } else {
          this.statusPwd = true
        }
      },
      confirmName () {
        if (this.username) {
          this.statusName = false
        } else {
          this.statusName = true
        }
      }
    }
  }
</script>

<style lang="less">
  .u-commit{
    width: 200px;
    height: 50px;
    display: inline-block;
    background: #FF5F54;
    border: none;
    color: #FFF;
    font-size: .8rem;
    border-radius: 5px;
    box-shadow: 0 2px 2px #FF2C26;
    margin-right: 10px;
  }
  .u-commit:hover{
    background: #FF1E0F;
  }
  .error-tip{
    border: 2px solid #FF708B;
    box-shadow: 2px -2px 2px #FFB9D4;
  }
</style>