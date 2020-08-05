<template>
  <div class="bg"  >
        <el-form    class="box" ref="form" :model="form" :rules="rules"label-width="70px">
            <el-form-item  label="登录名"  prop='account'>  
              <!--传入组件中的model中的字段   form中的属性-->
              <el-input class="input" placeholder="请输入用户名" v-model="form.account"></el-input>
            </el-form-item>
            <el-form-item label="密 码" prop='password'>
              <el-input  class="input"  placeholder="请输入密码" v-model="form.password" show-password></el-input>
            </el-form-item>
            
            <el-form-item  class="btn">
              <el-button @click="submitForm(form)" >登陆</el-button>
              <el-button  @click='resetForm(form)' class="child-btn">重置</el-button>
            </el-form-item>
      </el-form>
  </div>
</template>

<script>
import {login} from '@/api/article'
import {setToken} from '@/utils/token'

export default {
  name: 'login',
  data(){
    return{
       form: {
          account: 'admin',
          password: 'admin@123',
         
        },
        rules:{
          account:[
            { required: true, message: '请输入登录名', trigger: 'blur' },
            { min: 2, max: 8, message: '长度在 3到 8个字符', trigger: 'blur' }
          ],
            password:[
            { required: true, message: '请输入密码', trigger: 'blur' },
            { min: 3, max: 15, message: '长度在 3 到 15 个字符', trigger: 'blur' }
          ],
        
        }
    }
  },
  methods:{
      submitForm(form){
        this.$refs.form.validate((valid) => {
          if (valid) {
             login(this.form).then(res=>{
                console.log(res)
                if(res.data.code==20000){
                  setToken(res.data.data.token)
                  // console.log(res.data.data.token)
                  this.$router.push('/home')
                }
            })
           
          } else {
          console.log('error submit!!!')
          return false;
          }
        });
      },

      resetForm(form){
        this.$refs.form.resetFields();
      
  }
  }
}
</script>

<style scoped>

    .bg{
      display:flex;
      align-items: center;
      justify-content:center;
      position: relative;
      width:100%;
      height:704px;
      border:none;
      background:rgba(-195,132,149,0.2)
      /*background:url(../../assets/img/bg2.jpg) no-repeat;*/
      /*background-image:url(@/asset/img/login-bg.jpg)*/
    }
    .input{
      width:300px;
    }
    .btn{
      position:relative;
    }
    .btn .child-btn{
      position:absolute;
      right:36px;
    }
</style>
