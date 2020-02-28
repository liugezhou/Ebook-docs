<template>
  <div id="app">
    <el-form 
        style="width:500px"
        :inline ="false"
        :model="data" 
        :rules="rules" 
        ref="form"
        validate-on-rule-change
        status-icon
        label-width="100px"
        label-position="top"
        label-suffix=":"
        :disabled="false"
        size="medium"
        hide-required-asterisk
    >
      <el-form-item 
          label="审批人" 
          prop="user"
          :error="error"
          :validate-status='status'
          >
        <el-input v-model="data.user" placeholder="审批人" clearable></el-input>
      </el-form-item>
      <el-form-item label="活动区域">
        <el-select v-model="data.region" placeholder="活动区域" style="width:100%">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">查询</el-button>
        <el-button type="primary" @click="addRule">添加校验规则</el-button>
        <!-- <el-button type="success" @click="showSuccess">成功校验</el-button>
        <el-button type="danger" @click="showError">失败校验</el-button>
        <el-button type="primary" @click="showValidating">校验中</el-button> -->
      </el-form-item>
    </el-form>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      error:'这是一个自定义错误',
      status:'',
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
    showError() {
      this.status = 'error'
      this.error = '用户名输入有误'
    },
    showSuccess() {
      this.status = 'success'
      this.error = ''
    },
    showValidating() {
      this.status = 'validating'
      this.error = ''
    },
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