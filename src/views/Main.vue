<template>
    <div class="main">
        <el-container>
            <!-- 左侧的菜单栏 -->
            <el-aside width="200px">
                左侧边栏
            </el-aside>
            <!-- 右侧 -->
            <el-container>
                <!-- 顶部的信息栏 -->
                <el-header height="60px">
                    顶部
                </el-header>
                <!-- 主体部分 -->
                <el-main>
                    <router-view></router-view>
                </el-main>
            </el-container>
        </el-container>
    </div>
</template>
<script>
    export default {
        //create/mounte/update/destroy
        beforeCreate(){
            //组件创建之前先要检查是否已经登录为管理员
            if(!this.$store.state.adminName){
                //如果未登录跳转到login登录页面
                this.$router.push('/login');
            }
        }
    }
</script>

