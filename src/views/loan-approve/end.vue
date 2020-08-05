<template>
   
  <div class="app-container" style="margin-left:82px;">
    
    <div class="filter-container" style=" margin-bottom:15px ">
      <el-input v-model="listquery.name" placeholder="请输入姓名" style="width: 300px;  margin-right:10px" class="filter-item" 
      @input="query()" />
      <el-button class="filter-item" type="primary" icon="el-icon-search" @click="query()"  >
        搜索
      </el-button>
    </div>

    <el-table
    :data="tableData"
    style="width: 100%">
    <el-table-column
      type="index"
      label="序号"
      width="80px">
    </el-table-column>
    <el-table-column
      fixed
      prop="loan_name"
      label="姓名"
      width="100"
      column-key="loan_name"
      >
    </el-table-column>
    <el-table-column
      prop="loan_card"
      label="身份证号"
      width="250"
      >
    </el-table-column>
   
    
    <el-table-column label="操作" width="350">
      <template slot-scope="{row}">
        <el-button 
          size="mini" type="primary"
          @click="seevalue(row)" >查看</el-button>
        <el-button 
          size="mini"
         type="success" @click="successval(row)"
          >通过</el-button>
         <el-button
          size="mini"    type="danger" @click=" rejectval(row)"
          >拒绝</el-button>
        
      </template>
    </el-table-column>
  </el-table>
          
         <el-dialog
              title="用户信息"
              :visible.sync=" dialogFormVisible"
              width="80%"
              center>
              <el-form :model="temp"  ref="temp"  label-position="left" label-width="70px">
                 <el-card class="box-card" >
                <div slot="header" class="clearfix">
                  <span>个人基本信息</span>
                </div>
                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="姓名">
                      <el-input v-model="temp.name" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="出生日期">
                      <el-input v-model="temp.birthday"/>
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="性别">
                     <el-input  v-model="temp.sex" class="filter-item" />
                   </el-form-item>
                  </el-col>
                </el-row>
                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="身份证">
                      <el-input v-model.number="temp.identity_card" />
                       </el-form-item>
                   </el-col>
                   </el-row>
                 <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="婚姻状态" prop="marriage">
                      <el-input v-model="temp.marriage" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="教育程度" prop="education">
                      <el-input v-model="temp.education"  />
                   </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="居住地址" prop="address1">
                      <el-input v-model="temp.address1" />
                    </el-form-item>
                  </el-col>
                </el-row>

                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="户籍地址" prop="address2">
                      <el-input v-model="temp.address2" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="居住电话" prop="phone">
                      <el-input v-model.number="temp.phone" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="手机号" prop="mobile_phone">
                      <el-input v-model.number="temp.mobile_phone" />
                    </el-form-item>
                  </el-col>
                </el-row>
              </el-card>

               <!-- 职业信息 -->
            <el-card class="box-card">
                <div slot="header" class="clearfix">
                  <span>职业信息</span>
                </div>
                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="6" :lg="6">
                    <el-form-item label="现职公司全称" prop="company">
                      <el-input v-model="temp.company" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="6" :lg="6">
                    <el-form-item label="所属行业" prop="trade">
                       <el-input v-model="temp.trade" />
                    
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="6" :lg="6">
                    <el-form-item label="职位" prop="position">
                      <el-input v-model="temp.position" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="6" :lg="6">
                    <el-form-item label="公司地址" prop="address3">
                      <el-input v-model="temp.address3" />
                    </el-form-item>
                  </el-col>
                </el-row>

                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="公司类型" prop="company_type">
                      <el-input v-model="temp.company_type" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="公司邮箱" prop="company_email">
                      <el-input v-model="temp.company_email" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="公司电话" prop="company_phone">
                      <el-input v-model.number="temp.company_phone" />
                    </el-form-item>
                  </el-col>
                </el-row>
              </el-card>
              
              <!-- 收支情况 -->
           <el-card class="box-card">
                <div slot="header" class="clearfix">
                  <span>收支情况</span>
                </div>
                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="收支情况" prop="income">
                      <el-input v-model="temp.income" />
                    </el-form-item>
                  </el-col>
                </el-row>
              </el-card>
              
              <!-- 家庭联系人 -->
            <el-card class="box-card">
                <div slot="header" class="clearfix">
                  <span>家庭联系人</span>
                </div>
                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="关系1" prop="contact">
                      <el-input v-model="temp.contact" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="姓名" prop="contact_name">
                      <el-input v-model="temp.contact_name" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="手机" prop="contact_phone">
                      <el-input v-model.number="temp.contact_phone" />
                    </el-form-item>
                  </el-col>
                </el-row>
              </el-card>     

              <!-- 工作证明人 -->
              <el-card class="box-card">
                <div slot="header" class="clearfix">
                  <span>工作证明人</span>
                </div>
                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="关系2" prop="contact2">
                      <el-input v-model="temp.contact2" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="姓名" prop="contact2_name">
                      <el-input v-model="temp.contact2_name" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="手机" prop="contact2_phone">
                      <el-input v-model.number="temp.contact2_phone" />
                    </el-form-item>
                  </el-col>
                </el-row>

                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="部门" prop="contact2_dep">
                      <el-input v-model="temp.contact2_dep" />
                    </el-form-item>
                  </el-col>
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="职位" prop="contact2_pos">
                      <el-input v-model="temp.contact2_pos" />
                    </el-form-item>
                  </el-col>
                </el-row>

                <el-row :gutter="10">
                  <el-col :xs="24" :sm="12" :md="8" :lg="8">
                    <el-form-item label="备注">
                      <el-input v-model="temp.remark"  />
                    </el-form-item>
                  </el-col>
                </el-row>
        </el-card>
       </el-form>
       <div slot="footer" class="dialog-footer">
              <el-button @click="dialogFormVisible = false" type="primary">
                退出
              </el-button>
        </div>
  </el-dialog>

         <!--分页-->
      <div class="block" style=" margin-top:10px ">
        <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="listquery.pageNo"
            :page-sizes="[10, 20, 30, 40]"
            :page-size="listquery.pageSize"
            layout="total, sizes, prev, pager, next, jumper"
            :total="rows">
      </el-pagination>
      </div>
  </div>

</template>

<script>
import { approveendlist, endloanquery, approveendpass,approveendreject} from '@/api/article.js'
import { sexOptions,marriageOptions,educationOptions} from '@/utils/selectData.js'
 
export default {
  name: '',
  data(){
    return{
      // flagsuccess:true,
      dialogFormVisible:false,
     tableData: [], //表格展示的数据
      pages:1, //总页数
      rows:1, //总条数
      listquery:{
        pageNo:1,//当前页面
        pageSize:10,//条数
        name:'' //查询条件
      },
     temp:{
        name:'',//姓名
        identity_card:'',//身份证
        birthday:'',//出生日期
        sex:'',//性别
        marriage:'',//婚姻状态
        education:'',//教育程度
        address1:'',//居住地址
        address2:'',//户籍地址
        phone:'',//居住电话
        mobile_phone:'',//手机号
        company:'',//现职公司全称
        trade:'',//所属行业
        position:'',//职位
        address3:'',//公司地址
        company_type:'',//公司类型
        company_email:'',//公司邮箱
        company_phone:'',//公司电话
        income:'',//收支情况
        contact:'',//关系1
        contact_name:'',//姓名
        contact_phone:'',//手机
        contact2:'',//关系2
        contact2_name:'',//姓名
        contact2_phone:'',//手机
        ontact2_dep:'',//部门
        contact2_pos:'',//职位
        remark:''//备注
      },
      sexOptions,marriageOptions,educationOptions
      
      
    }
  },
  
    
  
   created() {  
    this.getlist();  //初始化获得数据
  },
  methods:{
    //当前条数变化
    handleSizeChange(val=this.listquery.pageSize ){
      this.listquery.pageSize = val;
      this.getlist();
    },
    //当前页变化
    handleCurrentChange(val=this.listquery.pageNo){
      this.listquery.pageNo = val;
      this.getlist();
    },
    getlist(){
        approveendlist(this.listquery).then(res=>{
         let {code} = res.data;
         console.log(res)
        
        if(code=='20000'){
             console.log(23456)
          let {data,rows,pages} = res.data.data.data;
            this.tableData = data;
            this.rows = rows;
            this.pages = pages;
        }
       }).catch(error=>{
          console.log(error)
       })
    },
    //查询数据
     query(){
      this.getlist()
    },
     //  查看信息
   seevalue(row){
      endloanquery({id:row.loan_id}).then(res=>{
         console.log(res)
         console.log(999)
           let {code} = res.data;
         if(code=='20000'){
            console.log(888)
           this.dialogFormVisible=true;
           this.temp=res.data.data.data
          // this.getlist();
         
        }
      })
    },
    //  审核通过
   successval(row){
       approveendpass({appId:row.id,loanId:row.loan_id}).then(res=>{
        let {code} = res.data;
        console.log(res)
        if(code=='20000'){
        this.getlist();
          this.$notify({  //通知框
            // title: '恭喜',
            message: '审核已提交',
            type:'success',
            duration: 2000
          });
        }
      })
    },

    //  审核拒绝
   rejectval(row){
       approveendreject({appId:row.id,loanId:row.loan_id}).then(res=>{
        let {code} = res.data;
         console.log(res)
        if(code=='20000'){
          //  console.log(3333)
          this.getlist();
          this.$notify({  //通知框
            // title: '审核失败',
            message:'审核提交成功',
            type:'success',
            duration: 2000
          });
        }
      })
    },
    
  

  }
}
</script>

<style scoped>

</style>
