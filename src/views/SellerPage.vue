<template>
  <div class="sellerpage">
    <a-row type="flex" :gutter="[24, 24]" justify="space-around" align="middle">
      <!-- Sign In Form Column -->
      <a-col
        :span="24"
        :md="10"
        :lg="{ span: 12, offset: 0 }"
        :xl="{ span: 6, offset: 2 }"
      >
        <h3 class="mb-10">매물 등록하기</h3>
        <p class="mb-40">
          등록을 원하시는 아파트를 찾아, 거래 정보를 입력하여 주세요.
        </p>

        <!-- Sign In Form -->
        <a-form id="components-form-demo-normal-login" :hideRequiredMark="true">
          <a-form-item
            class="font-semibold"
            label="[ 아파트정보 ] "
            :colon="false"
            ><a-row class="mb-10">
              <a-select
                v-model="sidocode"
                style="width: 100%"
                @change="sidoChange"
              >
                <a-select-option
                  v-for="(sido, index) in sidoList"
                  :key="index"
                  rowKey="index"
                  :value="sido.code"
                  >{{ sido.name }}
                </a-select-option>
              </a-select>
            </a-row>

            <a-row class="my-10">
              <a-select
                v-model="guguncode"
                style="width: 100%"
                @change="gugunChange"
              >
                <a-select-option
                  v-for="(gugun, index) in gugunList"
                  :key="index"
                  :value="gugun.code"
                  >{{ gugun.name }}
                </a-select-option>
              </a-select>
            </a-row>

            <a-row class="my-10">
              <a-select v-model="aptcode" style="width: 100%">
                <a-select-option
                  v-for="(apt, index) in aptlist"
                  :key="index"
                  :value="apt.aptCode"
                  >{{ apt.aptName }}
                </a-select-option>
              </a-select>
            </a-row>
            <span class="text-danger" v-if="!haveapt"
              >해당 지역은 매매가능한 아파트가 없습니다.</span
            ></a-form-item
          >

          <!-- <a-row class="my-10">
            <a-input
              placeholder="아파트 이름 검색"
              v-model="inputName"
              enter-button
              @search="search"
            >
            </a-input>
          </a-row> -->
        </a-form>
      </a-col>
    </a-row>
  </div>
</template>

<script>
import DrawHouseTable from "../components/MapComponent/DrawHouseTable";
import http from "@/api/http";

export default {
  components: {
    DrawHouseTable,
  },
  data() {
    return {
      centerSetting: false,
      sidoList: [{ code: "default", name: "시/도 선택" }],
      sidocode: "default",
      gugunList: [{ code: "default", name: "구/군 선택" }],
      guguncode: "default",
      aptlist: [{ code: "default", name: "아파트 선택" }],
      infos: [],
      // input apart name
      inputName: "",
      // filter

      aptcode: "아파트 선택",
      haveapt: true,
      data: [],
    };
  }, // end of data
  created() {
    this.getSidoList();
  },

  clickRecord: function (record) {
    console.log("clickrecord : ", record);
    let position = new kakao.maps.LatLng(
      this.clickRecord.lat,
      this.clickRecord.lng
    );
    this.map.setCenter(position);
  },

  methods: {
    getSidoList() {
      console.log("get sido list");
      http.get("/region/sido").then(({ data }) => {
        data.forEach((element) => {
          this.sidoList.push(element);
        });
      });
    },
    sidoChange() {
      console.log("sido change");
      const code = this.sidocode;
      this.gugunList = [{ code: "default", name: "구/군 선택" }];

      http.get("/region/gugun/" + code).then(({ data }) => {
        data.forEach((element) => {
          this.gugunList.push(element);
        });
      });
    },
    gugunChange() {
      this.haveapt = true;
      console.log("gugun change");
      // 다 넘겨서 spring 에서 앞에 다섯글자만 잘라
      const code2 = this.guguncode;
      this.aptlist = [{ code: "default", name: "아파트 선택" }];
      let now = this;
      http.get("/region/apt/" + code2).then(({ data }) => {
        console.log(data);
        if (data === "") {
          console.log("아파트가 없어요");
          now.haveapt = false;
        }
        Array.from(data).forEach((element) => {
          this.aptlist.push(element);
        });
      });
    },
  },
}; // end of export
</script>

<style lang="scss" scoped></style>
