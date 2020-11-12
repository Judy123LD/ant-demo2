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
            'name',
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
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  methods: {
    // 需要用到的方法
    handleSubmit(e) {
      e.preventDefault();
      this.form.validateFields((err, values) => {
        if (!err) {
          
          window.console.log("Received values of form: ", values);
          this.axios({
            method:'post',
            // api 是 http://127.0.0.1:8000 的简写
            url:'http://localhost:8081/loginIn',
            data:values
            }).then(res=>{
                console.log(res);
                console.log(res.data);
                if(res.data=="success"){
                    self.location.href="/" //跳转到主页面
                    // window.location.href="/" 

                    console.log("登陆成功！")
                }else{
                    alert("用户名或密码错误，请重新输入！")
                }



            }).catch(error=>{
                console.log(error);
            })

          // axios.post('http://localhost:8081/loginIn',ruleForm).then(function (response) {
          //     console.log(response);
          //           })

        }
      });
    }
  }
};
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
