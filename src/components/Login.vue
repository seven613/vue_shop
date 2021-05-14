<template>
  <div class="login-container">
    <div class="login_box">
      <!-- 头像区域 -->
      <div class="avatar_box">
        <img src="../assets/logo.png"
             alt="">
      </div>
      <!-- 登录标签区 -->
      <el-form class="login_form"
               :model="loginForm"
               :rules="loginFormRules"
               ref="loginFormRef"
               label-width="0px">
        <el-form-item prop="username">
          <!-- 用户名 -->
          <el-input placeholder="用户名"
                    prefix-icon="iconfont icon-user "
                    v-model="loginForm.username">
          </el-input>
        </el-form-item>

        <el-form-item prop="password">
          <!-- 密码 -->
          <el-input placeholder="密码"
                    prefix-icon="iconfont icon-3702mima"
                    type="password"
                    v-model="loginForm.password">
          </el-input>
        </el-form-item>

        <el-form-item class="btns">
          <!-- 确认按钮 -->
          <el-button type="primary"
                     @click="login">登录</el-button>
          <!-- 取消按钮 -->
          <el-button type="info"
                     @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      // 登陆绑定的数据
      loginForm: {
        username: 'zs',
        password: '123'
      },
      loginFormRules: {
        username: [
          { required: true, message: '请输入登录名称', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入登录名称', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    // 重置
    resetLoginForm () {
      this.$refs.loginFormRef.resetFields()
    },
    // 表单预验证
    login () {
      this.$refs.loginFormRef.validate(async valid => {
        if (!valid) return
        const { data: res } = await this.$http.post('login', this.loginForm)
        if (res.meta.status !== 200) {
          return this.$message.error('登录失败')
        } else {
          this.$message.success('登录成功！')
          // 1.将登录成功后的token，保存到客户端的sessionStorage中
          // 1.1 项目中除了登录之外的其他API接口，必须在登录之后才能访问
          // 1.2 token只应在当前网站打开期间生效，所以将token保存在sessionStorage中
          // 2.通过编程式导航跳转到后台主页，路由地址是/home

          window.sessionStorage.setItem('token', res.data.token)
          this.$router.push('/home')
        }
        console.log(res)
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login-container {
  background-color: #2b4b6b;
  height: 100%;
}

.login_box {
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);

  .avatar_box {
    height: 130px;
    width: 130px;
    border: 1px solid #eee;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 10px;
    position: absolute;
    left: 50%;
    transform: translate(-50%, -30%);
    background-color: #fff;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eee;
    }
  }
}

.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}

.btns {
  display: flex;
  justify-content: flex-end;
}
</style>
