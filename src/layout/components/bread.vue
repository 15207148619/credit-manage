<template>
  <div  class="bread">
    <ul>
        <li><router-link to="/home">首页</router-link></li>
        <li v-for="(v,i) in lists" :key="i" >
            <span v-if="i==0">/</span>
            <router-link :to="v.path"  > {{v.meta.title}}</router-link>
            <span v-if="i<(lists.length-1)">/</span>
        </li>
    </ul>
    <!-- 右侧下拉框 -->
    <div class="right-menu">
      <el-dropdown>
        <span class="el-dropdown-link">
          退出<i class="el-icon-arrow-down el-icon--right"></i>
        </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>
            <span style="display:block;" @click="goBack">退出</span>
          </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>  
</template>

<script>
// import {removeToken} from '@/utils/token'
// import {logout} from '@/api/article'
import {logout} from '@/api/api'
import {remove} from '@/tools/storage'

export default {
  name: '',
  data(){
    return{
        lists:[],
    }
  },
  methods:{
   goBack(){
      logout().then(()=>{
        this.$store.dispatch('logoutgoback')
        remove();  //删除token
        this.$router.push('/login');
      })
      
    }
  },
  watch: {
      $route(to,form){
          console.log(to);
           var matched=to.matched;
                if(matched.length&&matched[0].name=='layout'){
                    matched.splice(0,1)
                }
                if(matched.length&&matched[0].name=='home'){
                    matched.splice(0,1)
                }
               
                this.lists= matched;        
      }
  },
 
}
</script>

<style scoped>
    
    .bread ul li{
        display:inline-block;
     
    }
   
     .bread  .right-menu{
        float: right;
      margin-top:-37px;
     }
</style>
