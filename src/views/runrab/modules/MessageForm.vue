<template>
  <a-spin :spinning="confirmLoading">
    <j-form-container :disabled="formDisabled">
      <a-form-model ref="form" :model="model" :rules="validatorRules" slot="detail">
        <a-row>
          <a-col :span="24">
            <a-form-model-item label="留言用户" :labelCol="labelCol" :wrapperCol="wrapperCol" prop="userid">
              <a-input v-model="model.userid" placeholder="请输入留言用户"  ></a-input>
            </a-form-model-item>
          </a-col>
          <a-col :span="24">
            <a-form-model-item label="用户头像" :labelCol="labelCol" :wrapperCol="wrapperCol" prop="avatar">
              <j-image-upload class="avatar-uploader" text="上传" v-model="model.avatar" ></j-image-upload>
            </a-form-model-item>
          </a-col>
          <a-col :span="24">
            <a-form-model-item label="身份信息" :labelCol="labelCol" :wrapperCol="wrapperCol" prop="identity">
<!--              <a-input-number v-model="model.identity" placeholder="请输入身份信息" style="width: 100%" />-->
              <a-select v-model="model.identity" placeholder="请选择身份信息" style="width: 100%">
                <a-select-option value="1">教师</a-select-option>
                <a-select-option value="2">学生</a-select-option>
              </a-select>
            </a-form-model-item>
          </a-col>
          <a-col :span="24">
            <a-form-model-item label="可见性" :labelCol="labelCol" :wrapperCol="wrapperCol" prop="visible">
<!--              <a-input-number v-model="model.visible" placeholder="请输入可见性" style="width: 100%" />-->
              <a-select v-model="model.visible" placeholder="请选择可见性" style="width: 100%">
                <a-select-option value="0">本人可见</a-select-option>
                <a-select-option value="1">全部可见</a-select-option>
              </a-select>
            </a-form-model-item>
          </a-col>
          <a-col :span="24">
            <a-form-model-item label="留言内容" :labelCol="labelCol" :wrapperCol="wrapperCol" prop="context">
              <a-textarea v-model="model.context" rows="4" placeholder="请输入留言内容" />
            </a-form-model-item>
          </a-col>
        </a-row>
      </a-form-model>
    </j-form-container>
  </a-spin>
</template>

<script>

  import { httpAction, getAction } from '@/api/manage'
  import { validateDuplicateValue } from '@/utils/util'

  export default {
    name: 'MessageForm',
    components: {
    },
    props: {
      //表单禁用
      disabled: {
        type: Boolean,
        default: false,
        required: false
      }
    },
    data () {
      return {
        model:{
         },
        labelCol: {
          xs: { span: 24 },
          sm: { span: 5 },
        },
        wrapperCol: {
          xs: { span: 24 },
          sm: { span: 16 },
        },
        confirmLoading: false,
        validatorRules: {
        },
        url: {
          add: "/runrab/message/add",
          edit: "/runrab/message/edit",
          queryById: "/runrab/message/queryById"
        }
      }
    },
    computed: {
      formDisabled(){
        return this.disabled
      },
    },
    created () {
       //备份model原始值
      this.modelDefault = JSON.parse(JSON.stringify(this.model));
    },
    methods: {
      add () {
        this.edit(this.modelDefault);
      },
      edit (record) {
        this.model = Object.assign({}, record);
        this.visible = true;
      },
      submitForm () {
        const that = this;
        // 触发表单验证
        this.$refs.form.validate(valid => {
          if (valid) {
            that.confirmLoading = true;
            let httpurl = '';
            let method = '';
            if(!this.model.id){
              httpurl+=this.url.add;
              method = 'post';
            }else{
              httpurl+=this.url.edit;
               method = 'put';
            }
            httpAction(httpurl,this.model,method).then((res)=>{
              if(res.success){
                that.$message.success(res.message);
                that.$emit('ok');
              }else{
                that.$message.warning(res.message);
              }
            }).finally(() => {
              that.confirmLoading = false;
            })
          }

        })
      },
    }
  }
</script>