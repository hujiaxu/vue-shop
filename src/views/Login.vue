<template>
  <div class="LoginContainer">
    <div class="LoginBox">
      <el-form ref="LoginRef" :model="LoginForm" :rules="LoginRules" class="Login-form">
        <!-- 用户名 -->
        <el-form-item prop="username">
          <el-input v-model="LoginForm.username" prefix-icon="iconfont icon-user"></el-input>
        </el-form-item>
        <!-- 密码 -->
        <el-form-item prop="password">
          <el-input v-model="LoginForm.password" prefix-icon="iconfont icon-3702mima" type="password"></el-input>
        </el-form-item>
        <!-- 按钮 -->
        <el-form-item class="btns">
          <el-button type="success" @click="Login">登录</el-button>
          <el-button type="info" @click="RefClick">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      // 这是登录表单数据绑定对象
      LoginForm: {
        username: 'admin',
        password: '123456'
      },
      LoginRules: {
        username: [
          {
            required: true,
            message: '请输入登录名称',
            trigger: 'blur'
          },
          {
            min: 3,
            max: 10,
            message: '长度在 3 到 10 之间',
            trigger: 'blur'
          }
        ],
        password: [
          {
            required: true,
            message: '请输入登录密码',
            trigger: 'blur'
          },
          {
            min: 5,
            max: 10,
            message: '长度在 5 到 10 之间',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    // 重置登录信息按钮
    RefClick() {
      console.log(this)
      return this.$refs.LoginRef.resetFields()
    },
    Login() {
      return this.$refs.LoginRef.validate(async valid => {
        if (!valid) return
        const { data: res } = await this.$http.post('login', this.LoginForm)
        if (res.meta.status !== 200) return this.$message.error('登录失败')
        this.$message.success('登录成功')
        window.sessionStorage.setItem('token', res.data.token)
        this.$router.push('/home')
      })
    }
  }
}
</script>

<style lang="less" scoped>
  .LoginContainer {
    height: 100%;
    background-color: #2b4b6b;
      .LoginBox {
      position: relative;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 450px;
      height: 300px;
      background-color: #fff;
      border-radius: 6px;
        .Login-form {
          position: absolute;
          bottom: 0;
          padding: 0 20px;
          box-sizing: border-box;
          width: 100%;
            .btns {
              display: flex;
              justify-content: flex-end;
            }
        }
    }
  }
</style>
