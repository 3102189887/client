<template>
  <div
    class="login-wrap"
    style="height: 100vh;
  display: flex; align-items: center;
  justify-content: center;

"
  >
    <div
      style="display: flex; background-color: white; width: 54%; border-radius: 5px; overflow: hidden"
    >
      <div style="flex: 1">
        <img src="@/assets/img/16.png" alt="" style="width: 450px;height: 400px" />
      </div>
      <div
        style="flex: 1; display: flex; align-items: center; justify-content: center"
      >
        <el-form :model="formData" style="width: 80%" :rules="rules" ref="form">
          <div
            style="font-size: 20px; font-weight: bold; text-align: center; margin-bottom: 20px"
          >
            欢迎登录教务管理(课程管理)系统
          </div>
          <el-form-item prop="username">
            <!--必须绑定v-model输入框才能输入字符---->
            <el-input
              v-model="formData.username"
              placeholder="学号/工号/用户名"
              autocomplete="off"
            >
              <i slot="prefix" class="el-input__icon el-icon-user"></i>
            </el-input>
          </el-form-item>

          <el-form-item prop="password">
            <el-input
              v-model="formData.password"
              size="medium"
              placeholder="请输入密码"
              clearable
              show-password
              autocomplete="off"
            >
              <i slot="prefix" class="el-input__icon el-icon-lock"></i>
            </el-input>
          </el-form-item>
          <el-form-item prop="userType">
            <el-radio-group v-model="formData.userType" label-width="100%">
              <el-radio-button label="1">学生</el-radio-button>
              <el-radio-button label="2">教师</el-radio-button>
              <el-radio-button label="3">教务管理员</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <!--          <el-form-item prop="userType">-->
          <!--            <el-radio-group v-model="formData.userType">-->
          <!--              <el-radio label="1">学生</el-radio>-->
          <!--              <el-radio label="2">教师</el-radio>-->
          <!--              <el-radio label="3">教务管理员</el-radio>-->
          <!--            </el-radio-group>-->
          <!--          </el-form-item>-->
          <el-form-item>
            <el-button type="primary" style="width: 100%" @click="submit()"
              >登 录</el-button
            >
          </el-form-item>
      

        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
import { login } from "../api/user";

export default {
  data: function() {
    return {
      formData: {
        username: "",
        password: "",
        userType: "1",
      },
      rules: {
        username: [
          { required: true, message: "请输入用户名", trigger: "blur" },
        ],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }],
        userType: [
          { required: true, message: "请选择用户类型", trigger: "blur" },
        ],
      },
    };
  },
  methods: {
    submit() {
      this.$refs.form.validate((valid) => {
        if (valid) {
          login(
            this.formData.username,
            this.formData.password,
            this.formData.userType
          ).then((res) => {
            this.$message.success("登录成功: " + res.username);
            this.$store.commit("login", res);
            this.$router.push({ name: "container" });
          });
        }
      });
    },
  },
};
</script>

<style scoped>
.login-wrap {
  position: relative;
  width: 100%;
  height: 100%;
  /* background: #0f9876; */
  background-color: #5a83c9;
  background-image: url("../assets/img/login-bg.svg");
  background-size: 100% 100%;
}

.form-title {
  width: 100%;
  line-height: 50px;
  text-align: center;
  font-size: 20px;
  color: #fff;
  border-bottom: 1px solid #ddd;
}

.login-form {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 350px;
  margin: -190px 0 0 -175px;
  border-radius: 5px;
  background: rgba(0, 0, 0, 0.6);
  overflow: hidden;
}

.form-content {
  padding: 30px 30px;
}

.login-btn {
  text-align: center;
}

.login-btn button {
  width: 100%;
  height: 36px;
}

.el-radio {
  color: #fff;
}
</style>
