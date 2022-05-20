<!-- 
	This is the sign in page, it uses the dashboard layout in: 
	"./layouts/Default.vue" .
 -->

<template>
  <div class="sign-in">
    <a-row type="flex" :gutter="[24, 24]" justify="space-around" align="middle">
      <!-- Sign In Form Column -->
      <a-col
        :span="24"
        :md="10"
        :lg="{ span: 12, offset: 0 }"
        :xl="{ span: 6, offset: 2 }"
        class="col-form"
      >
        <h3>Sign In</h3>
        <h5 class="font-regular text-muted">
          Enter your id and password to sign in
        </h5>

        <!-- Sign In Form -->
        <a-form
          id="components-form-demo-normal-login"
          :form="form"
          class="login-form"
          :hideRequiredMark="true"
        >
          <a-form-item class="mb-10" label="id" :colon="false">
            <a-input
              v-decorator="[
                'id',
                {
                  rules: [{ required: true, message: 'Please input your id!' }],
                },
              ]"
              v-model="user.userid"
              placeholder="id"
            />
          </a-form-item>
          <a-form-item class="mb-5" label="Password" :colon="false">
            <a-input
              v-decorator="[
                'password',
                {
                  rules: [
                    { required: true, message: 'Please input your password!' },
                  ],
                },
              ]"
              type="password"
              v-model="user.userpass"
              placeholder="Password"
            />
          </a-form-item>
          <a-form-item class="mb-10">
            <a-switch v-model="rememberMe" /> Remember Me
          </a-form-item>
          <a-form-item>
            <a-button
              type="primary"
              block
              class="login-form-button"
              @click="loginBtn"
            >
              SIGN IN
            </a-button>
          </a-form-item>
        </a-form>
        <!-- / Sign In Form -->

        <p class="font-semibold text-muted">
          Don't have an account?
          <router-link to="/sign-in" class="font-bold text-dark"
            >Sign Up</router-link
          >
        </p>
      </a-col>
      <!-- / Sign In Form Column -->

      <!-- Sign In Image Column
			<a-col :span="24" :md="12" :lg="12" :xl="12" class="col-img">
				<img src="images/img-signin.jpg" alt="">
			</a-col> -->
      <!-- Sign In Image Column -->
    </a-row>
  </div>
</template>

<script>
const memberStore = "memberStore";
import { mapState, mapActions } from "vuex";
export default {
  data() {
    return {
      // Binded model property for "Sign In Form" switch button for "Remember Me" .
      user: {
        userid: "",
        userpass: "",
      },
      rememberMe: true,
    };
  },
  beforeCreate() {
    // Creates the form and adds to it component's "form" property.
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  computed: {
    ...mapState(memberStore, ["isLogin"]),
  },
  methods: {
    ...mapActions(memberStore, ["userConfirm", "getUserInfo"]),

    async loginBtn() {
      console.log("로그인할 사용자 : " + this.user.userid);
      await this.userConfirm(this.user);
      let token = sessionStorage.getItem("access-token");
      //로그인 됬으면,
      if (this.isLogin) {
        //console.log("로그인 되었음 ");
        await this.getUserInfo(token);
        this.$router.push({ name: "Home" });
      }
    },
    // Handles input validation after submission.
    // handleSubmit(e) {
    //   e.preventDefault();
    //   this.form.validateFields((err, values) => {
    //     if (!err) {
    //       console.log("Received values of form: ", values);
    //     }
    //   });
    // },
  },
};
</script>

<style lang="scss">
body {
  background-color: #ffffff;
}
</style>
