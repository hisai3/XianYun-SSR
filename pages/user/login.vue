<template>
  <div class="container">
    <!-- 主要内容 -->
    <el-row type="flex" justify="center" align="middle" class="main">
      <div class="form-wrapper">
        <!-- 表单头部tab -->
        <el-row type="flex" justify="center" class="tabs">
          <span
            :class="{active: currentTab === index}"
            v-for="(item, index) in [`登录`, `注册`]"
            :key="index"
            @click="handleChangeTab(index)"
          >{{item}}</span>
        </el-row>

        <!-- 登录功能组件 -->
        <!-- <LoginForm v-if="currentTab == 0"/> -->
        <el-form :model="form" ref="form" :rules="rules" class="form" v-if="currentTab == 0">
          <el-form-item class="form-item" prop="username">
            <el-input placeholder="用户名/手机" v-model="form.username"></el-input>
          </el-form-item>

          <el-form-item class="form-item" prop="password">
            <el-input placeholder="密码" type="password" v-model="form.password"></el-input>
          </el-form-item>

          <p class="form-text">
            <nuxt-link to="#">忘记密码</nuxt-link>
          </p>

          <el-button class="submit" type="primary" @click="handleLoginSubmit">登录</el-button>
        </el-form>

        <!-- 注册功能组件 -->
        <!-- <RegisterForm v-if="currentTab == 1"/> -->
        <RegisterForm v-if="currentTab == 1"></RegisterForm>
      </div>
    </el-row>
  </div>
</template>

<script>
import RegisterForm from '@/components/user/RegisterForm.vue'
export default {
  components:{
    RegisterForm
  },
  data() {
    return {
      currentTab: 0,
      // 表单数据
      form: {
        username: "", // 登录用户名/手机
        password: "" // 登录密码
      },
      // 表单规则
      rules: {
        username: [
          {
            required: true,
            message: "请输入用户名",
            trigger: "blur"
          }
        ],
        password: [
          {
            required: true,
            message: "请输入密码",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    handleChangeTab(index) {
      this.currentTab = index;
    },
    // 提交登录
    handleLoginSubmit() {
      // 验证表单
      this.$refs["form"].validate(valid => {
         // 为true表示没有错误
            if (valid) {
                // 删除代码
                // this.$axios({
                //     url: "/accounts/login",
                //     method: "POST",
                //     data: this.form
                // }).then(res => {
                //     console.log(res.data);
                // })

                // 新增代码
                this.$store.dispatch("user/login", this.form).then(res => {
                    // 成功提示
                    this.$message({
                        message: "登录成功，正在跳转",
                        type: "success"
                    });
                    // 跳转到首页
                    setTimeout(() => {
                        this.$router.replace("/")
                    }, 1000);
                })
            }
      });
    }
  }
};
</script>
<style scoped lang="less">
.container {
  background: url(http://157.122.54.189:9095/assets/images/th03.jfif) center 0;
  height: 700px;
  min-width: 1000px;

  .main {
    width: 1000px;
    height: 100%;
    margin: 0 auto;
    position: relative;

    .form-wrapper {
      width: 400px;
      margin: 0 auto;
      background: #fff;
      box-shadow: 2px 2px 0 rgba(0, 0, 0, 0.1);
      overflow: hidden;

      .tabs {
        span {
          display: block;
          width: 50%;
          height: 50px;
          box-sizing: border-box;
          border-top: 2px #eee solid;
          background: #eee;
          line-height: 48px;
          text-align: center;
          cursor: pointer;
          color: #666;

          &.active {
            color: orange;
            border-top-color: orange;
            background: #fff;
            font-weight: bold;
          }
        }
      }
    }
  }
}
.form {
  padding: 25px;
}

.form-item {
  margin-bottom: 20px;
}

.form-text {
  font-size: 12px;
  color: #409eff;
  text-align: right;
  line-height: 1;
}

.submit {
  width: 100%;
  margin-top: 10px;
}
</style>