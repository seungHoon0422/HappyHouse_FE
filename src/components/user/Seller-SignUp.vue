<template>
  <div>
    <h5 class="font-semibold text-center">Register With</h5>
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
          placeholder="Name"
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
        >
        </a-input>
        &nbsp; @ &nbsp;
        <a-select default-value="naver.com" style="width: 170px">
          <a-select-option value="naver.com">naver.com </a-select-option>
          <a-select-option value="ssafy.com">ssafy.com </a-select-option>
          <a-select-option value="google.com">google.com </a-select-option>
          <a-select-option value="daum.com"> daum.net </a-select-option>
        </a-select>
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
        >
        </a-input>
      </a-form-item>
      <a-form-item label="휴대폰" class="mb-10">
        <a-input
          style="width: 350px"
          v-decorator="[
            'phone',
            {
              rules: [{ required: true, message: 'Please input your phone!' }],
            },
          ]"
          placeholder="phone"
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
        >
          SIGN UP
        </a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
