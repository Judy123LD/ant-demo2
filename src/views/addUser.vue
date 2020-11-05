<template>
   <div align="center">
       <h1>新增用户</h1>
     <a-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" laba-width="100px" class="demo-ruleForm"
     style="width:300px;margin-top:30px">
         <a-form-item label="用户名" prop="name">
             <a-input  v-model="ruleForm.name" ></a-input>
         </a-form-item>
         <a-form-item label="密码" prop="password">
             <a-input v-model="ruleForm.password"></a-input>
         </a-form-item>
         <a-form-item>
             <a-button type="primary" @click="submitForm('ruleForm')">提交</a-button>
             <a-button @click="resetForm('ruleForm')">重置</a-button>
         </a-form-item>
     </a-form>
 </div>  
</template>

<script>
    export default {
        name: "Adduser",
        data() {
            var validateName = (rule, value, callback) => {
                if (value === '') {
                    callback(new Error('请输入用户名'));
                } else {
                    if (this.ruleForm.name !== '') {
                        //如果不为空
                    }
                    callback();
                }
            };
            var validatepassword = (rule, value, callback) => {
                if (value === '') {
                    callback(new Error('请输入密码'));
                } else {
                    if (this.ruleForm.password !== '') {
                        //如果不为空
                    }
                    callback();
                }
            };
            return {
                ruleForm: {
                    name: '',
                    password: ''
                },
                rules: {
                    name: [
                        { validator: validateName, trigger: 'blur' }
                    ],
                    password: [
                        { validator: validatepassword, trigger: 'blur' }
                    ]
                }
            };
        },
        methods: {
            submitForm(formName) {
                var that=this;
                // this.$refs[formName].validate((valid) => {
                    this.$refs[formName].validateFields((err, values) => {
                    if (valid) {
                        //提交成功后要做的事情
                        // alert('submit!');
                        console.log(that.ruleForm)
                        axios.post('http://localhost:8081/addUser/',that.ruleForm).then(function (response) {
                            console.log(response);
                        })
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            }
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

