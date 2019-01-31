<template>
    <div class="settings">
        <el-breadcrumb>
            <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
            <el-breadcrumb-item>全局设置</el-breadcrumb-item>
        </el-breadcrumb>

        <el-card shadow="never">
            <el-form :model="formData" label-width="110px">
                <el-form-item label="应用名称：">
                    <el-input v-model="formData.appName"></el-input>
                </el-form-item>
                <el-form-item label="应用API网址：">
                    <el-input v-model="formData.apiUrl"></el-input>
                </el-form-item>
                <el-form-item label="后台管理段网址：">
                    <el-input v-model="formData.adminUrl"></el-input>
                </el-form-item>
                <el-form-item label="客户端App网址：">
                    <el-input v-model="formData.appUrl"></el-input>
                </el-form-item>
                <el-form-item label="ICP备案号：">
                    <el-input v-model="formData.icp"></el-input>
                </el-form-item>
                <el-form-item label="版权声明：">
                    <el-input v-model="formData.copyright"></el-input>
                </el-form-item>

                <el-form-item>
                    <el-button type="primary" @click="doSubmit">保存修改</el-button>
                    <el-button @click="doCancel">取消修改</el-button>
                </el-form-item>
            </el-form>
        </el-card>
    </div>
</template>
<script>
    export default {
       data(){
           return {
               formData:{

               }
           }
       },
       mounted(){
           //将$store存储中的全局配置数据赋值给中间变量-formData,方便表单元素执行双向数据绑定
           //引用复制，两个变量指向同一个对象
           this.formData=JSON.parse(JSON.stringify(this.$store.state.globalSettings));
       },
       methods:{
           doSubmit(){
               var url=this.$store.state.globalSettings.apiUrl+'/admin/settings';
               var data=this.formData;
               this.$axios.put(url,data).then((res)=>{
                   if(res.data.code==200){
                       this.$message.success('全局设置修改成功!');
                       //修改$store中的全局设置！！！
                       this.$store.commit('setGlobalSettings',data);
                   }else{
                       this.$message.error('全局设置修改失败!');
                   }
               }).catch((err)=>{
                   console.log(err);
               });
           },
           doCancel(){
               this.formData=JSON.parse(JSON.stringify(this.$store.state.globalSettings));
           }
       }
    }
</script>

