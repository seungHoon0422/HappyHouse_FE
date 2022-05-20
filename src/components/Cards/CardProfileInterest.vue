<template>
  <!-- Conversations Card -->
  <a-card
    :bordered="false"
    class="header-solid h-full card-profile-information"
    :bodyStyle="{ paddingTop: 0, paddingBottom: '16px' }"
    :headStyle="{ paddingRight: 0 }"
  >
    <template #title>
      <h6 class="font-semibold m-0 pl-10">나의 관심목록</h6>
    </template>
    <ul>
      <li v-for="(interest, index) in interests" :key="index">
        {{ interest.aptname }}
      </li>
    </ul>
  </a-card>
  <!-- / Conversations Card -->
</template>

<script>
import { mapState } from "vuex";
import http from "@/api/http";
const memberStore = "memberStore";

export default {
  data() {
    return {
      interests: [],
    };
  },
  created() {
    let userid = this.userInfo.userid;
    http.get("/interest/" + userid).then(({ data }) => {
      console.log(data);
      data.forEach((element) => {
        let interest = {
          aptname: element,
        };
        this.interests.push(interest);
        console.log(this.interests);
      });
    });
  },
  computed: {
    ...mapState(memberStore, ["userInfo"]),
  },
};
</script>
