<template>
  <div class="app-login-duanxin">
    <form action="" @submit.prevent="submit" class="form">
          <p><input type="text" placeholder="输入手机号" class="tell" v-model="tellinfo"  maxlength="11"/><span class="del" v-show="show" @click="del">×</span></p>
          <p><input type="text" placeholder="输入验证码" class="yazhe n" v-model="yazhen"><span :class="flag" >获取验证码</span></p>
          <p><input type="submit" value="登录" class="submit"></p>
    </form>
    <p class="message">未注册用户，系统自动为您注册</p>
  
  </div>
</template>

<script>
import axios from 'axios'
import {Toast} from "mint-ui"
import {mapActions} from "vuex"

export default {
  name: 'AppLoginDuanxin',
  data() {
    return {
      tellinfo:'',
      yazhen:'',
      imgs:[],
      flag:"yzinfo",
      show: false
    }
  },
  watch: {
    tellinfo() {
      if(this.tellinfo != "") {
        this.show = true
      }     
      if(this.tellinfo.length == 11){
            this.flag = "action"
      }else{
        this.flag= "yzinfo"
      }
    }
  },
  methods: {
    ...mapActions(['register']),
    del() {
        this.tellinfo = ''
        this.show = false
    },
    submit(){
      let that = this
      // let res = /^1[34578]\d{9}$/
      if(this.tellinfo && this.yazhen) {
        this.register({username:this.tellinfo,password:this.yazhen})
      }else if(this.tellinfo.length==0){
        Toast({
          message:"手机号不能为空",
          duration:1500,
          iconClass: "icon iconfont icon-Group"
        })
      }else if(this.yazhen.length ==0){
         Toast({
          message:"密码不能为空",
          duration:1500,
          iconClass: "icon iconfont icon-Group"
        })
      }
    }
  }

}
</script>
<style lang="scss">
    .mint-toast {
      position: fixed;
      max-width: 85%;
      border-radius: 5px;
      background: rgba(0, 0, 0, 0.6);
      color: #fff;
      box-sizing: border-box;
      text-align: center;
      z-index: 1000;
      -webkit-transition: opacity .3s linear;
      transition: opacity .3s linear;
        .mint-toast-icon {
            display: block;
            text-align: center;
            font-size: 0.22rem;
            color: #e23333;
        }
    }
    
</style>

<style scoped lang="scss">
.app-login-duanxin {
  width: 100%;
  box-sizing: border-box;
  background: #fff; 
  padding-bottom: 0.5rem;  
  .form {
    width: 100%;  
    p {
      width: 100%; 
      padding: 0 0.27rem;
      position: relative; 
      input {
        width: 100%;       
        border: none;
        height: 0.5rem;
        border-bottom: 1px solid #ccc;
        outline: none;
        font-size: 0.16rem;
      }
      .yzinfo {
        position: absolute;
        right: 0;
        bottom: 0.1rem;
        background: #eee;
        color: #ccc;
        font-size: 0.16rem;
        width: 0.9rem;
        height: 0.3rem;
        text-align: center;
        line-height:0.3rem;
        border-radius: 0.1rem;
      }
      .del {
        position: absolute;
        right: 0;
        bottom: 0.1rem;
        font-size: 0.2rem; 
        background: #eee;
        width: 0.25rem;
        height: 0.25rem;
        text-align: center;
        line-height: 0.25rem;
        border-radius: 50%;
      }
      .submit {
        margin-top: 0.3rem;
        height: 0.6rem;
        background: #c3dcb3;
        color: #fff;
        font-size: 0.2rem;
        border-radius: 0.3rem;
      }
    }
  }
  .message {
    font-size: 0.2rem;
    color: #ccc;
    margin-top: 0.2rem;
    text-align: center;
  }
  .action {
      position: absolute;
      right: 0;
      bottom: 0.1rem;
      font-size: 0.16rem;
      width: 0.9rem;
      height: 0.3rem;
      text-align: center;
      line-height:0.3rem;
      border-radius: 0.1rem;
      background: #6eb042;
      color: #fff;
  }
 
  //  .iconfont {
  //   font-size: 0.14rem!important;
  //   color: #e23333!important;
  // }
 
}
</style>
