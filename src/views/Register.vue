<template>
  <div align="center">
    <div style="font-size:30px;margin-top:50px">研究生实习实践管理平台</div>

    <a-form
      id="components-form-demo-normal-register"
      :form="form"
      style="width:300px;margin-top:30px"
      class="register-form"
      @submit="handleSubmit"
    >
      <!-- <a-form-item>
        <a-input
          v-decorator="[
            'phoneNumber',
            { rules: [{ required: true, message: '请输入手机号' }] }
          ]"
          placeholder="手机号"
        >
          <a-icon slot="prefix" type="phone" style="color: rgba(0,0,0,.25)" />
        </a-input>
      </a-form-item>
      <a-form-item>
        <a-input
          v-decorator="[
            'email',
            { rules: [{ required: true, message: '请输入邮箱' }] }
          ]"
          placeholder="邮箱"
        >

        </a-input>
      </a-form-item> -->
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
        <a-button type="primary" html-type="submit" class="register-form-button">
          注册
        </a-button>

        <router-link class="login" :to="{ name: 'Login' }"
          >登录
        </router-link>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {
  beforeCreate() {
    this.form = this.$form.createForm(this, { name: "normal_register" });
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
            url:'http://localhost:8081/register',
            data:values
            }).then(res=>{
                console.log(res);
                console.log(res.data);
                if(res.data=="success"){
                    self.location.href="/login" //跳转到登录页面
                    // window.location.href="/" 
                     alert("注册成功！")
                    console.log("注册成功！")
                }else if(res.data=="username existed"){
                    alert("用户名已存在，请重新输入！")
                }else{
                   alert("注册失败，请再试一次！")
                }

            }).catch(error=>{
                console.log(error);
            })

          // axios.post('http://localhost:8081/registerIn',ruleForm).then(function (response) {
          //     console.log(response);
          //           })

        }
      });
    }
  }
};
</script>

<style>
#components-form-demo-normal-register .register-form {
  /* max-width: 300px; */
  width: 300px;
}
#components-form-demo-normal-register .register-form-forgot {
  float: right;
}
#components-form-demo-normal-register .register-form-button {
  width: 100%;
}
</style>
