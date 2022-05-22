<template>
  <div>
    <h5 class="font-semibold text-center">비밀번호 찾기</h5>
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
      <a-form-item label="아이디" class="mb-5">
        <a-input
          style="width: 350px"
          v-decorator="[
            '아이디',
            {
              rules: [{ required: true, message: 'Please input your id!' }],
            },
          ]"
          placeholder="id"
          v-model="userid"
        >
        </a-input>
      </a-form-item>
      <a-form-item>
        <a-button
          type="primary"
          block
          html-type="submit"
          class="login-form-button"
          @click="findpw"
        >
          비밀번호찾기
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
      username: "",
      userid: "",
    };
  },
  beforeCreate() {
    // Creates the form and adds to it component's "form" property.
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  methods: {
    findpw() {
      let userid = this.userid;
      let username = this.username;
      http
        .get("/restuser/findpass/" + userid + "/" + username)
        .then(function (response) {
          if (response.data === "") {
            alert("아이디와 이름을 확인하여 주세요 !! ");
          } else {
            alert(response.data);
          }
        });
      console.log("비밀번호 찾기");
    },
  },
};
</script>

<style lang="scss"></style>
