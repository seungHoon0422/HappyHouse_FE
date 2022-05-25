<template>
  <div>
    <h5 class="font-semibold text-center">비밀번호 찾기</h5>
    <a-form
      id="components-form-demo-normal-login"
      :label-col="{ span: 5 }"
      class="login-form"
    >
      <a-modal :visible="visible" title="비밀번호 변경">
        <template #footer>
          <a-button key="cancel" @click="handleCancel">취소</a-button>
          <a-button key="ok" @click="changepass">확인</a-button>
        </template>

        <a-form>
          <a-form-item>
            <a-input addon-before="새 비밀번호" v-model="userpass" />
            <br />
            <span class="ml-30 text-danger" v-if="!passinput"
              >새로운 비밀번호를 입력하여 주세요.</span
            >
          </a-form-item>
          <a-form-item>
            <a-input addon-before="새 비밀번호 확인 " v-model="userpasscheck" />
            <span class="ml-30 text-danger" v-if="!newpassinput"
              >이름을 입력하여 주세요.</span
            >
          </a-form-item>
        </a-form>
      </a-modal>

      <a-form-item label="이름" class="my-30">
        <a-input style="width: 350px" placeholder="name" v-model="username">
        </a-input>
        <span class="ml-30 text-danger" v-if="!nameinput"
          >이름을 입력하여 주세요.</span
        >
      </a-form-item>
      <a-form-item label="아이디" class="my-30">
        <a-input style="width: 350px" placeholder="id" v-model="userid">
        </a-input>
        <span class="ml-30 text-danger" v-if="!idinput"
          >아이디를 입력하여 주세요.</span
        >
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
      passinput: true,
      newpassinput: true,
      visible: false,
      username: "",
      userid: "",
      userpass: "",
      userpasscheck: "",
      nameinput: true,
      idinput: true,
    };
  },
  beforeCreate() {
    // Creates the form and adds to it component's "form" property.
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  methods: {
    changepass() {
      this.passinput = true;
      this.newpassinput = true;
      if (!this.userpass) {
        this.passinput = false;
      }
    },
    handleCancel() {
      this.visible = false;
    },
    findpw() {
      this.nameinput = true;
      this.idinput = true;
      if (!this.username) {
        this.nameinput = false;
      }
      if (!this.userid) {
        this.idinput = false;
      }
      let userid = this.userid;
      let username = this.username;
      let result = "";
      http
        .get("/restuser/findpass/" + userid + "/" + username)
        .then(function (response) {
          result = response.data;
          if (response.data === "") {
            alert("회원정보가 존재하지 않습니다");
            return;
          } else {
          }
        });
    },
  },
};
</script>

<style lang="scss"></style>
