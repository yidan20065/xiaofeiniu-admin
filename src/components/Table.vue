<template>
    <div class="xfn-table-info">
        <el-card shadow="hover">
            <div class="xfn-table"></div>
            <el-button type="success" plain size="mini">详情</el-button>
            <el-button type="danger" plain size="mini">修改</el-button>
        </el-card>
    </div>
</template>
<script>
    export default {
        props:['data']
    }
</script>
<style lang="scss">

</style>
