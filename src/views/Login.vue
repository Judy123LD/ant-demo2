<template>
  <div align="center">
    <div style="font-size:30px;margin-top:50px">研究生实习实践管理平台</div>

    <a-form
      id="components-form-demo-normal-login"
      :form="form"
      style="width:300px;margin-top:30px"
      class="login-form"
      @submit="handleSubmit"
    >
      <a-form-item>
        <a-input
          v-decorator="[
            'username',
            { rules: [{ required: true, message: '请输入用户名' }] }
          ]"
          placeholder="用户名"
        >
          <a-icon slot="prefix" type="user" style="color: rgba(0,0,0,.25)" />
        </a-input>
      </a-form-item>
      <a-form-item>
        <a-input
          v-decorator="[
            'password',
            { rules: [{ required: true, message: '请输入密码' }] }
          ]"
          type="password"
          placeholder="密码"
        >
          <a-icon slot="prefix" type="lock" style="color: rgba(0,0,0,.25)" />
        </a-input>
      </a-form-item>

      <a-form-item>
        <a-button type="primary" html-type="submit" class="login-form-button">
          登录
        </a-button>

        <router-link class="register" :to="{ name: 'Register' }"
          >注册账户
          </router-link>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {
    beforeCreate() {
    this.form = this.$form.createForm(this, { name: 'normal_login' })
  },
  methods:{
    // 需要用到的方法
    handleSubmit(e) {
      e.preventDefault()
      this.form.validateFields((err, values) => {
        if (!err) {
          window.console.log('Received values of form: ', values)
              //用户名密码传给后端
              // let res=loginCheck
              //           ({"username":values.username,
              //             "password":values.password,
              //             })

                res=1 //暂时先写死
              // 账号密码正确
              if(res==1){
                // window.location.href="/overview" 
                window.console.log('账号密码正确')
              }
              //账号密码错误
              else{
                  alert("账号或密码错误，请重新输入！")
              } 
        

           

        }
      })
    },
}
}
</script>

<style>
#components-form-demo-normal-login .login-form {
  /* max-width: 300px; */
  width: 300px;
}
#components-form-demo-normal-login .login-form-forgot {
  float: right;
}
#components-form-demo-normal-login .login-form-button {
  width: 100%;
}
</style>
