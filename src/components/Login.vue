<template>
  <div class="login">

    <van-form @submit="handleLogin">
      <h2 class="title">和信后台管理系统-员工端</h2>
      <van-cell-group inset>
        <van-field
            v-model="loginForm.username"
            name="用户名"
            label="用户名"
            placeholder="用户名"
            :rules="[{ required: true, message: '请填写用户名' }]"
        />
        <van-field
            v-model="loginForm.password"
            type="password"
            name="密码"
            label="密码"
            placeholder="密码"
            :rules="[{ required: true, message: '请填写密码' }]"
        />
      </van-cell-group>
      <div style="margin: 16px;">
        <van-button round block   type="primary" native-type="submit">
          登录
        </van-button>
      </div>
    </van-form>

  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Login',
  props: {
    msg: String
  },
  data(){
    return{
      loginForm:{
        username:'',
        password:'',
        // rememberMe:false
      },
      loading:false
    }
  },
  methods:{
    handleLogin(){

      //设置Vuex登录标志为true，默认userLogin为false
      this.$store.dispatch("userLogin", true);
      //Vuex在用户刷新的时候userLogin会回到默认值false，所以我们需要用到HTML5储存
      //我们设置一个名为Flag，值为isLogin的字段，作用是如果Flag有值且为isLogin的时候，证明用户已经登录了。
      localStorage.setItem("Flag", "isLogin");
      //iViewUi的友好提示
      //登录成功后跳转到指定页面
      this.$router.push("/index");

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.login {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  /*background-image: url("../assets/images/login-background.jpg");*/
  background-size: cover;
}
.login-form {
  border-radius: 6px;
  background: #ffffff;
  width: 400px;
  padding: 25px 25px 5px 25px;
}
</style>
