<template>
  <div class="form-group">

    <el-form>
      <el-form-item label="问题">
        <el-input type="textarea" autosize placeholder="随便问点啥问题" v-model="form.questionTextarea"></el-input>
      </el-form-item>
      <el-form-item label="回答">
        <el-input type="textarea" autosize placeholder="这里是回答" v-model="form.answerTextarea"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">提交</el-button>
        <el-button>取消</el-button>
      </el-form-item>
    </el-form>



    <el-upload
            action="http://localhost:3000/question_answer/upload_pictures"
            :file-list="fileList">
      <el-button size="small" type="primary">点击上传</el-button>
      <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
    </el-upload>

  <el-upload
    action="https://jsonplaceholder.typicode.com/posts/"
    :file-list="fileList">
    <el-button size="small" type="primary">点击上传</el-button>
    <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
  </el-upload>

  </div>
</template>



<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data(){
    return {
      form: {
        questionTextarea:'',
        answerTextarea:'',
      },
      fileList:[]
    }
  },
  props: {
    msg: String
  },
  // async created(){
  //   let response = await axios.get("http://localhost:3000",{a:"adawdadawd"},{
  //     header:{
  //
  //     }
  //   })
  // },
  methods: {
    onSubmit(){
      console.log(this.form.questionTextarea);
      console.log(this.form.answerTextarea);

      if(this.form.questionTextarea && this.form.answerTextarea){
        axios.post('http://localhost:3000/question_answer/insert', {
          question: this.form.questionTextarea,
          answer: this.form.answerTextarea
        }).then((res)=>{
          console.log(res);
        }).catch((err)=>{
          console.log(err);
        });
      }else{
        this.openNotification();
      }

    },
    openNotification(){
      const h = this.$createElement;
      this.$notify({
        titile: '没有输入完啦',
        message: h('i', { style: 'color: teal'}, '请填写问题和答案！不要留空')
      });
    }
  }
}
</script>
