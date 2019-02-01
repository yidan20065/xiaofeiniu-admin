<template>
    <div class="xfn-table-info">
        <el-card shadow="hover">
            <div class="xfn-table" :style="{background:getTableColor(data.status)}">
                {{data.tid}}号桌:{{data.status|tableStatus}}</div>
            <el-button type="success" plain size="mini" @click="showTableDetail">详情</el-button>
            <el-button type="danger" plain size="mini">修改</el-button>
        </el-card>
        <!-- 桌台详情对话框 -->
        <el-dialog :title="data.tid+'号桌台详情'" 
        :visible="dialogTableDetailVisible" 
        :before-close="closeDialogTableDetail"
        >
            <!-- 对话框主体 -->
            <el-tabs type="border-card" @tab-click="makeQRCode">
                <el-tab-pane label="桌台状态">状态加载中...</el-tab-pane>
                <el-tab-pane label="桌台二维码">
                    <!-- <canvas id="qrcanvas"></canvas> -->
                    <img :src="qrcodeData" />
                </el-tab-pane>
            </el-tabs>

            <div slot="footer">
                <el-button type="primary" @click="dialogTableDetailVisible=false">确定</el-button>
            </div>
        </el-dialog>
    </div>
</template>
<script>
    export default {
        data(){
            return {
                dialogTableDetailVisible:false,
                qrcodeData:''
            }
        },
        props:['data'],
        methods:{
            getTableColor(status){
                if(status==1) return '#67C23A';
                else if(status==2) return '#E6A23C';
                else if(status==3) return '#F56C6C';
                else return '#909399';
            },
            showTableDetail(){
                //console.log(this.data);  //当前桌子的数据
                this.dialogTableDetailVisible=true;
            },
            closeDialogTableDetail(){
                this.dialogTableDetailVisible=false;
            },
            makeQRCode(){
                //创建二维码，
                var qrcode=require('qrcode');
                var tableUrl=this.$store.state.globalSettings.apiUrl+'/#/'+this.data.tid;
                console.log(tableUrl)
                qrcode.toDataURL(tableUrl,{
                    width:300,
                    errorCorrectionLevel:'H'
                },(err,url)=>{
                   this.qrcodeData=url;
                })
            }
        }
    }
</script>
<style lang="scss">
    .xfn-table-info{
        padding: 3px;
        text-align: center;
        .xfn-table{
            width: 90%;
            height: 150px;
            line-height: 150px;
            border: 1px solid #aaa;
            box-shadow: 3px -4px 5px #666;
            margin: 5px auto;
            border-radius: 50%;
        }
    }
</style>
