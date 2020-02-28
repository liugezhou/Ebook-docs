<template>
  <div id="app">
    <el-form 
        inline 
        :model="data" 
        :rules="rules" 
        ref="form"
        :validate-on-rule-change="false"
    >
      <el-form-item label="审批人" prop="user">
        <el-input v-model="data.user" placeholder="审批人" clearable></el-input>
      </el-form-item>
      <el-form-item label="活动区域">
        <el-select v-model="data.region" placeholder="活动区域">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">查询</el-button>
        <el-button type="primary" @click="addRule">添加校验规则</el-button>
      </el-form-item>
    </el-form>
    <hand-validate></hand-validate>
  </div>
</template>

<script>
import handValidate from './components/handValidate'
export default {
  name: 'app',
  components:{
    handValidate
  },
  data() {
    return {
      data: {
        user: '',
        region: ''
      },
      rules: {
        user: [
          { required: true, trigger: 'blur', message: '用户名必须录入' }
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      console.log(this.data)
    },
    addRule() {
    const userValidator = (rule, value, callback) => {
      if (value.length > 3) {
        this.inputError = ''
        this.inputValidateStatus = ''
        callback()
      } else {
        callback(new Error('用户名长度必须大于3'))
      }
    }
    const newRule = [
      ...this.rules.user,
      { validator: userValidator, trigger: 'change' }
      ]
      this.rules = Object.assign({}, this.rules, { user: newRule })
    }
  }
}
</script>