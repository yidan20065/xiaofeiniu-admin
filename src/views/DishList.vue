<template>
    <div class="dishlist">
        <h2>菜品类别</h2>
        <el-tabs type="border-card">
            <el-tab-pane v-for="(c,i) in dishList" :key="i" >
                <span slot="label">
                    <el-badge :value="c.dishList.length">{{c.cname}}</el-badge>
                </span>

                <el-row>
                    <el-col v-for="(d,j) in c.dishList" :key="j"
                    :xs="12" :md="6" :lg="4" :xl="3">
                    {{d.title}}
                    <img :src="require('../assets/img/dish/'+d.imgUrl)" style="max-width:100%" />
                    </el-col>
                </el-row>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>
<script>
    export default {
       data(){
           return{
               dishList:[]
           }
       },
       mounted(){
           //异步获取菜品列表
           var url=this.$store.state.globalSettings.apiUrl+'/admin/dish';
           this.$axios.get(url).then(({data})=>{
               this.dishList=data;
           }).catch((err)=>{
               console.log(err);
           })
       }
    }
</script>
