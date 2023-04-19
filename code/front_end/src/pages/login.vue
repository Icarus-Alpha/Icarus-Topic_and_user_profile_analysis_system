<template>
  <div class="yqLogin">
    <div class="container switch">
      <!-- 注册页面 -->
      <div class="container-form container-signup">
        <form action="javascript:void(0);" class="form">
          <h2 class="form-title">注册</h2>
          <input
            type="text"
            placeholder="用户名"
            class="input"
            v-model="sign_up_user"
          />
          <input
            type="email"
            placeholder="电子邮箱"
            class="input"
            v-model="email"
          />
          <input
            type="password"
            placeholder="密码"
            class="input"
            v-model="sign_up_password"
          />
          <button class="submit" @click="SignUp">注册</button>
        </form>
      </div>
      <!-- 登录页面 -->
      <div class="container-form container-signin">
        <form action="javascript:void(0);" class="form">
          <h2 class="form-title">登录</h2>
          <input
            type="text"
            placeholder="用户名"
            class="input"
            v-model="sign_in_user"
          />
          <input
            type="password"
            placeholder="密码"
            class="input"
            v-model="sign_in_password"
          />
          <font size="1" class="passwordsize">
          <a href="javascript:void(0);">忘记你的密码？</a>
          </font>
          <button class="submit" @click="SignIn">登录</button>
        </form>
      </div>
      <!-- 覆盖层 -->
      <div class="container-overlay">
        <div class="overlay">
          <div class="overlay-slide overlay-left">
            <button class="submit" id="goSignIn">注册</button>
          </div>
          <div class="overlay-slide overlay-right">
            <button class="submit" id="goSignUp">登录</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      all_info: "",
      sign_in_user: "",
      sign_in_password: "",
      sign_up_user: "",
      sign_up_password: "",
      email: "",
    };
  },
  mounted() {
    this.switch();
    this.getUserInfo();
  },
  methods: {
    getUserInfo() {
      this.$axios.get("user.json").then((res) => {
        this.all_info = res.data;
      });
    },
    switch() {
      // 我们需要获取两个切换按钮 因此需要到 html 结构中 定义特殊类名或 id 名
      const goSignIn = document.querySelector("#goSignIn");
      const goSignUp = document.querySelector("#goSignUp");
      // 获取被切换的样式类
      const container = document.querySelector(".container");
      // 添加点击事件
      goSignIn.addEventListener("click", () => {
        container.classList.remove("switch");
      });
      goSignUp.addEventListener("click", () => {
        container.classList.add("switch");
      });
    },
    SignUp() {
      this.getUserIngo();
      let sign_up_info = {};
      sign_up_info.user = this.sign_up_user;
      sign_up_info.password = this.sign_up_password;
      sign_up_info.email = this.email;
      this.$axios
        .put("user/" + this.sign_up_user + ".json", sign_up_info)
        .then(() => {
          this.sign_up_user = "";
          this.sign_up_password = "";
          this.email = "";
        });
      this.$message({
        showClose: true,
        message: "恭喜你，注册成功",
        type: "success",
      });
    },
    SignIn() {
      this.getUserInfo();
      //flag: 0 未找到账户 flag: 1 账户存在密码不对 flag: 2 账户密码都正确
      let flag = 0;
      Object.keys(this.all_info).forEach((key) => {
        if (this.sign_in_user == key) {
          flag = 1;
          if (this.sign_in_password == this.all_info[key].password) {
            flag = 2;
          }
        }
      });
      if (flag == 0) {
        this.$message({
          showClose: true,
          message: "未找到该用户",
          type: "error",
        });
      }
      if (flag == 1) {
        this.$message({
          showClose: true,
          message: "密码错误",
          type: "error",
        });
      }
      if (flag == 2) {
        this.$message({
          showClose: true,
          message: "登录成功",
          type: "success",
        });
        let user_info = {
          user:this.sign_in_user,
          password:this.sign_in_password
        }
        user_info = JSON.stringify(user_info)
        localStorage.setItem("token",user_info)
        this.$router.push({path:'/home'})
      }
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}
/* 清除 input、button 默认边框以及点击高亮 */
input,
button {
  outline: none; 
  border: none;
}
/* 清除 a 标签默认下划线 颜色设置为#333 */
a {
  text-decoration: none;
  color: #333;
  margin: 1.25rem 0;
}
/* 页面整体样式 */
.yqLogin {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: url("https://www.helloimg.com/images/2023/04/19/oXuGXt.png")
    no-repeat fixed center;
  background-size: cover;
}
/* 盒子样式 */
.container {
  position: relative;
  width: 50%;
  height: 70vh;
  background-color: #080e1542;
  box-shadow: 0 1rem 1.5rem rgba(0, 0, 0, 0.3),
    0 0.5rem 0.5rem rgba(0, 0, 0, 0.2);
  border-radius: 1rem;
  overflow: hidden;
}
/* 将两个 form 表单设置绝对定位 */
.container-form {
  position: absolute;
  top: 0;
  height: 100%;
  transition: all 0.5s ease-in-out;
}
/* 设置注册页样式 */
.container-signin {
  left: 0;
  width: 50%;
  z-index: 1;
  opacity: 0;
}
/* 设置登录页样式 */
.container-signup {
  left: 0;
  width: 50%;
  z-index: 2;
  opacity: 1;
}
/* 默认显示 signup 注册页，通过操作 switch 类名 显示登录页 */
.container.switch .container-signin {
  transform: translateX(100%);
  z-index: 5;
  opacity: 1;
}
.container.switch .container-signup {
  transform: translateX(100%);
  opacity: 0;
}
/* 设置覆盖层 */
.container-overlay {
  position: absolute;
  left: 50%;
  top: 0;
  width: 50%;
  height: 100%;
  overflow: hidden;
  transform: translateX(0);
  transition: transform 0.5s ease-in-out;
  z-index: 999;
}
/* 设置显示背景图 */
.overlay {
  position: absolute;
  top: 0;
  left: -100%;
  width: 200%;
  height: 100%;
  background: url("https://www.helloimg.com/images/2023/04/19/oXuGXt.png")
    no-repeat fixed center;
  background-size: cover;
  transition: transform 0.5s ease-in-out;
}
/* 默认左边显示 通过操作 switch 类名显示登录页 */
.container.switch .container-overlay {
  transform: translateX(-100%);
}
.container.switch .overlay {
  transform: translateX(50%);
}
/* 设置切换按钮页样式 */
.overlay-slide {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 50%;
  transition: transform 0.5s ease-in-out;
}
.overlay-left {
  transform: translateX(-20%);
}
.overlay-right {
  transform: translateX(0);
  right: 0;
}
.container.switch .overlay-left {
  transform: translateX(0);
}
.container.switch .overlay-right {
  transform: translateX(20%);
}
/* 设置表单内元素样式 */
.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  padding: 0 1rem;
}
/* 设置 input 标签样式 */
.input {
  top: 0;
  width: 100%;
  height: 8%;
  margin: 0.5rem 0;
  padding: 1rem;
  border-radius: 2rem;
  max-width: 220px;
  border-radius: 12px;
  color: #ffffff;
  border: 1.5px solid lightgrey;
  outline: none;
  transition: all 0.3s cubic-bezier(0.19, 1, 0.22, 1);
  box-shadow: 0px 0px 20px -18px;
}
.input:hover {
  border: 2px solid lightgrey;
  box-shadow: 0px 0px 20px -17px;
}
.input:active {
  transform: scale(0.95);
}
.input:focus {
  border: 2px solid grey;
}

/*设置忘记密码在表格中占的尺寸*/
.passwordsize{
  width: 100%;
  height: 8%;
  margin: 0.5rem 0;
  padding: 1rem;
  max-width: 240px;
  color: #c6c3c3;
}
/* 设置表单标题样式 */
.form-title {
  font-weight: 300;
  margin-bottom: 1rem;
  color: #c6c3c3;
}

/* 只设置表单按钮的外边距 */
.form > .submit {
  margin-top: 1.5rem;
}
/* 设置按钮按下样式 */

/*登录按钮 */
button {
  padding: 1.3em 5em;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 2.5px;
  font-weight: 500;
  color: #000;
  background-color: #fff;
  border: none;
  border-radius: 45px;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease 0s;
  cursor: pointer;
  outline: none;
}

button:hover {
  background-color: #23c483;
  box-shadow: 0px 15px 20px rgba(46, 229, 157, 0.4);
  color: #fff;
  transform: translateY(-7px);
}

button:active {
  transform: translateY(-1px);
}
</style>