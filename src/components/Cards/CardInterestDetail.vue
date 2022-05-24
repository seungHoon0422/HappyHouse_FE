<template>
  <a-card
    :bordered="false"
    class="header-solid h-full card-profile-information"
    :bodyStyle="{ paddingTop: 0, paddingBottom: '16px' }"
    :headStyle="{ paddingRight: 0 }"
    :customRow="clickrow"
  >
    <template #title>
      <h6 class="font-semibold bg-gray-3 m-0 pl-10">
        {{ aptname }}
      </h6>

      <br />
      <div v-if="aptname">
        <div>
          <h10 class="font-regular text-gray-9 m-0 pl-10">{{
            sidodetail.sidoName +
            " " +
            sidodetail.gugunName +
            " " +
            sidodetail.dongName
          }}</h10>
          <p>
            <router-link class="pl-10" to="/billing"
              >-> 지도에서 찾아보기</router-link
            >
          </p>
          <a-col
            :span="24"
            style="
              display: flex;
              align-items: center;
              justify-content: flex-end;
            "
          >
            <a-button size="small" @click="deleteInterest">Delete</a-button>
          </a-col>
        </div>
      </div>
      <div v-else>
        <p>아파트를 선택하여 주세요</p>
      </div>
    </template>
    <br />
    <a-table :columns="columns" :data-source="data" :pagination="true">
    </a-table>
  </a-card>
</template>

<script>
import http from "@/api/http";
import { mapState } from "vuex";
const memberStore = "memberStore";
export default {
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    aptname: {
      type: String,
      default: () => [],
    },

    sidodetail: {
      type: Object,
    },
    columns: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      // detailInterest: [],
    };
  },
  // watch: {
  //   data: function (newData, oldData) {
  //     this.data = newData;
  //   },
  //   data: function (newData, oldData) {
  //     this.sidodetail = newData;
  //   },
  // },
  computed: {
    ...mapState(memberStore, ["userInfo"]),
  },
  methods: {
    clickrow: function (record, index) {
      return {
        on: {
          click: () => {
            console.log("아파트클릭", this.aptname);
          },
        },
      };
    },
    deleteInterest() {
      if (confirm(this.aptname + "을 관심목록에서 삭제하시겠습니까 ? ")) {
        let userid = this.userInfo.userid;
        console.log(userid + " " + this.aptname);
        http
          .delete("/interest/" + this.aptname + "/" + userid)
          .then(({ data }) => {
            console.log(data);
            this.$emit("deleteInterest", this.aptname);

            //     window.location.reload();
          });
      }
    },
  },
};
</script>

<style></style>
