<template>
    <div class="dishadd">
        <h2>添加菜品</h2>
        <el-form label-width="100px">
            <el-form-item label="菜品图片:">
                <el-upload class="xfn-upload"
                :action="uploadAction"
                :on-success="doUploadSucc"
                name="dishImg"
                :show-file-list="false">
                    <img v-if="imageUrl" :src="imageUrl" >
                </el-upload>
            </el-form-item>
        </el-form>
    </div>
</template>
<script>
    export default {
        data(){
            return{
                imageUrl:'', //要显示的预览图地址
                //可处理上传文件的数据API
                uploadAction:this.$store.state.globalSettings.apiUrl+'/admin/dish/image',
                formData:{
                    title:'',
                    imgUrl:'',  //菜品图片在服务器上的随机文件名
                    price:'',
                    detail:'',
                    categoryId:''
                }
            }
        },
        methods:{
            doUploadSucc(res,file){
                //文件上传成功后，客户端得到响应消息之后的处理函数
                console.log(res);
                this.formData.imgUrl=res.fileName;
                this.imageUrl=URL.createObjectURL(file.raw);
                //把上传的文件编码为DataURL字符串
            }
        }
    }
</script>
<style lang="scss">
    .xfn-upload{
        .el-upload{
            border: 1px dotted #aaa;
            border-radius: 3px;
            cursor: pointer;
            width: 250px;
            height: 177px;
            overflow: hidden;
            &:hover{
                border-color: #409eff;
            }
        }

        img{
            max-width: 100%;
        }
    }
</style>

