<template>
  <div>
    <el-form :model="LoginForm" ref="LoginForm" :rules="rules" class="loginContainer">
      <h3 class="loginTitle">系统登录</h3>
      <el-form-item label="用户名" prop="username">
        <el-input
          type="text"
          v-model="LoginForm.username"
          placeholder="请输入用户名"
          autocomplete="off"
        ></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input
          type="password"
          v-model="LoginForm.password"
          placeholder="请输入密码"
          autocomplete="off"
        ></el-input>
      </el-form-item>
      <el-form-item label="验证码" prop="verifycode">
        <el-input
          type="text"
          v-model="LoginForm.verifycode"
          placeholder="点击图片更换验证码"
          autocomplete="off"
          style="width: 200px; margin-right: 5px"
        ></el-input>
        <img :src="captchaUrl" />
      </el-form-item>
      <el-checkbox v-model="checked" class="loginRemember">记住我</el-checkbox>
      <el-button type="primary" style="width: 100%" @click="submitLogin()"
        >登录</el-button
      >
    </el-form>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      captchaUrl: "",
      LoginForm: {
        username: "admin",
        password: "123",
        verifycode: "",
      },
      checked: true,
      rules: {
        username: [
          { required: true, message: "请输入用户名", trigger: "blur" },
          {
            min: 3,
            max: 15,
            message: "用户名长度在3到15个字符",
            trigger: "blur",
          },
        ],
        password: [
          { required: true, message: "请输入密码", trigger: "blur" },
          {
            min: 3,
            max: 15,
            message: "密码长度在3到15个字符",
            trigger: "blur",
          },
        ],
        verifycode: [{ required: true, message: "请输入验证码", trigger: "blur" }],
      },
    };
  },
  props: {},
  created() {},
  methods: {
    submitLogin() {
      this.$refs.LoginForm.validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          this.$message.error("请输入所有必填字段！");
          return false;
        }
      });
    },
  },
};
</script>

<style lang="less">
.loginContainer {
  border-radius: 15px;
  background-clip: padding-box;
  margin: 180px auto;
  width: 350px;
  padding: 15px 35px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}
.loginTitle {
  margin: 0px auto 10px auto;
  text-align: center;
}
.loginRemember {
  text-align: left;
  margin: 0px 0px 15px 0px;
}
</style>
