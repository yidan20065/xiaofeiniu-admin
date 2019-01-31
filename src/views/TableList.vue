<template>
    <div class="xfn-table-list">
        <el-breadcrumb>
            <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
            <el-breadcrumb-item>桌台管理</el-breadcrumb-item>
            <el-breadcrumb-item>桌台列表</el-breadcrumb-item>
        </el-breadcrumb>
        <br>
        <!--响应式的桌台列表 -->
        <el-row>
            <el-col v-for="(t,i) in tableList" :key="i" 
             :xs="12" :sm="8" :md="6"
             :lg="4" :xl="2">
                <xfn-table :data="t"></xfn-table>
            </el-col>
        </el-row>
    </div>
</template>
<script>
    import Table from '../components/Table.vue'
    export default {
        data(){
            return {
                tableList:[]
            }
        },
        components:{
           'xfn-table':Table
        }
    }
</script>
<style lang="scss">

</style>
