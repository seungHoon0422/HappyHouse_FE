<template>
  <div>
    <!-- <template>
      <h5 class="font-semibold text-center">Register With</h5>
    </template>
    <div class="sign-up-gateways">
      <a-button>
        <img src="images/logos/logos-facebook.svg" alt="" />
      </a-button>
      <a-button>
        <img src="images/logos/logo-apple.svg" alt="" />
      </a-button>
      <a-button>
        <img src="images/logos/Google__G__Logo.svg.png" alt="" />
      </a-button>
    </div>
    <p class="text-center my-25 font-semibold text-muted">Or</p> -->
    <h5 class="font-semibold text-center">Register With</h5>
    <a-form
      id="components-form-demo-normal-login"
      :label-col="{ span: 5 }"
      class="login-form"
    >
      <a-form-item label="중개사무소명" class="mb-10">
        <a-input
          style="width: 350px"
          v-decorator="[
            'name',
            {
              rules: [{ required: true, message: 'Please input your name!' }],
            },
          ]"
          placeholder="Name"
          v-model="username"
        >
        </a-input>
      </a-form-item>
      <a-form-item label="아이디" class="mb-10">
        <a-input
          style="width: 350px"
          v-decorator="[
            'id',
            {
              rules: [{ required: true, message: 'Please input your id!' }],
            },
          ]"
          placeholder="id"
          v-model="userid"
        >
        </a-input>
      </a-form-item>
      <a-form-item label="비밀번호" class="mb-5">
        <a-input
          style="width: 350px"
          v-decorator="[
            'password',
            {
              rules: [
                { required: true, message: 'Please input your Password!' },
              ],
            },
          ]"
          type="password"
          placeholder="Password"
          v-model="userpass"
        >
        </a-input>
      </a-form-item>
      <a-form-item label="이메일" class="mb-10">
        <a-input
          style="width: 150px"
          v-decorator="[
            'email',
            {
              rules: [{ required: true, message: 'Please input your email!' }],
            },
          ]"
          placeholder="Email"
          v-model="emailid"
        >
        </a-input>
        &nbsp; @ &nbsp;
        <a-select v-model="emaildomain" style="width: 170px">
          <a-select-option value="naver.com">naver.com </a-select-option>
          <a-select-option value="ssafy.com">ssafy.com </a-select-option>
          <a-select-option value="google.com">google.com </a-select-option>
          <a-select-option value="daum.com"> daum.net </a-select-option>
        </a-select>
      </a-form-item>
      <a-form-item label="전화번호" class="mb-10">
        <a-input
          style="width: 350px"
          v-decorator="[
            'phone',
            {
              rules: [{ required: true, message: 'Please input your phone!' }],
            },
          ]"
          placeholder="02-xxx-xxxx"
          v-model="phone"
        >
        </a-input>
      </a-form-item>

      <a-form-item class="mb-10">
        <a-checkbox
          v-decorator="[
            'remember',
            {
              valuePropName: 'checked',
              initialValue: true,
            },
          ]"
        >
          I agree the
          <a href="#" class="font-bold text-dark">Terms and Conditions</a>
        </a-checkbox>
      </a-form-item>

      <a-form-item>
        <a-button
          type="primary"
          block
          html-type="submit"
          class="login-form-button"
          @click="sellerregist"
        >
          SIGN UP
        </a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
import http from "@/api/http";
export default {
  data() {
    return {
      userid: "",
      username: "",
      userpass: "",
      phone: "",
      emailid: "",
      emaildomain: "",
    };
  },
  beforeCreate() {
    // Creates the form and adds to it component's "form" property.
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  methods: {
    sellerregist() {
      let email = this.emailid + "@" + this.emaildomain;
      let phone = this.phone1 + "-" + this.phone2 + "-" + this.phone3;
      http
        .post("/restuser/regist", null, {
          params: {
            userid: this.userid,
            username: this.username,
            userpass: this.userpass,
            email: email,
            phone: this.phone,
            level: 1,
          },
        })
        .then(function (response) {
          alert(response.data);
        });
      this.$router.push({ name: "Sign-In" });
    },
  },
};
</script>

<style lang="scss"></style>
