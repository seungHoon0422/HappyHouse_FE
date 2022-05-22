<template>
  <div>
    <h5 class="font-semibold text-center">아이디 찾기</h5>
    <a-form
      id="components-form-demo-normal-login"
      :label-col="{ span: 5 }"
      class="login-form"
    >
      <a-form-item label="이름" class="mb-10">
        <a-input
          style="width: 350px"
          v-decorator="[
            'name',
            {
              rules: [{ required: true, message: 'Please input your name!' }],
            },
          ]"
          placeholder="name"
          v-model="username"
        >
        </a-input>
      </a-form-item>
      <a-form-item label="이메일" class="mb-5">
        <a-input
          style="width: 350px"
          v-decorator="[
            'email',
            {
              rules: [{ required: true, message: 'Please input your email!' }],
            },
          ]"
          placeholder="email"
          v-model="email"
        >
        </a-input>
      </a-form-item>
      <a-form-item>
        <a-button
          type="primary"
          block
          html-type="submit"
          class="login-form-button"
          @click="findid"
        >
          아이디 찾기
        </a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
import http from "@/api/http";
import { EvalSourceMapDevToolPlugin } from "webpack";
export default {
  data() {
    return {
      username: "",
      email: "",
    };
  },
  beforeCreate() {
    // Creates the form and adds to it component's "form" property.
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  methods: {
    findid() {
      let username = this.username;
      let email = this.email;
      http
        .get("/restuser/findid/" + username + "/" + email)
        .then(function (response) {
          if (response.data === "") {
            alert("이름과 이메일을 확인하여 주세요 !! ");
          } else {
            alert(response.data);
          }
        });
      console.log("아이디 찾기");
    },
  },
};
</script>

<style lang="scss"></style>
