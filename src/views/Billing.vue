<!-- 
	This is the billing page, it uses the dashboard layout in: 
	"./layouts/Dashboard.vue" .
 -->

<template>
  <div>
    <!--------------------------------- Search Bar  --------------------------------->
    <a-row :gutter="24" style="margin-bottom: 20px">
      <!--------------------------------- sido select  --------------------------------->
      <a-col :span="6">
        <a-select v-model="sidocode" style="width: 100%" @change="sidoChange">
          <a-select-option
            v-for="(sido, index) in sidoList"
            :key="index"
            rowKey="index"
            :value="sido.code"
            >{{ sido.name }}
          </a-select-option>
        </a-select>
      </a-col>
      <!--------------------------------- /sido select  --------------------------------->
      <!--------------------------------- gugun select  --------------------------------->
      <a-col :span="6">
        <a-select v-model="guguncode" style="width: 100%" @change="gugunChange">
          <a-select-option
            v-for="(gugun, index) in gugunList"
            :key="index"
            :value="gugun.code"
            >{{ gugun.name }}
          </a-select-option>
        </a-select>
      </a-col>
      <!--------------------------------- /gugun select  --------------------------------->
      <!--------------------------------- input  --------------------------------->
      <a-col :span="6">
        <a-input-search
          placeholder="아파트 이름 검색"
          enter
          enter-button
          @click="search"
        >
        </a-input-search>
      </a-col>

      <a-col :span="2">
        <a-button type="primary" style="margin-bottom: 0px" @click="search"
          >search</a-button
        >
      </a-col>

      <!--------------------------------- /input  --------------------------------->

      <!--------------------------------- search  --------------------------------->
    </a-row>
    <!--------------------------------- /search  --------------------------------->
    <a-row :gutter="24" style="margin-bottom: 20px">
      <a-col :span="1">
        <h5><strong>Filter</strong></h5>
      </a-col>

      <a-col :span="2">
        <a-row style="text-align: center"><h6>평수</h6></a-row>
        <a-select v-model="areaFilter" default-value="all" style="width: 100%">
          <a-select-option value="all"> 전체 </a-select-option>
          <a-select-option value="0"> 20평이하 </a-select-option>
          <a-select-option value="20"> 20평대 </a-select-option>
          <a-select-option value="30"> 30평대 </a-select-option>
          <a-select-option value="40"> 40평이상 </a-select-option>
        </a-select>
      </a-col>
      <a-col :span="2">
        <a-row style="text-align: center"><h6>층수</h6></a-row>
        <a-select v-model="floorFilter" default-value="all" style="width: 100%">
          <a-select-option value="all"> 전체 </a-select-option>
          <a-select-option value="0"> 5층 미만 </a-select-option>
          <a-select-option value="20"> 5층 이상 </a-select-option>
          <a-select-option value="30"> 10층 이상 </a-select-option>
        </a-select>
      </a-col>
      <a-col :span="2">
        <a-row style="text-align: center"><h6>매매가격</h6></a-row>
        <a-select
          v-model="dealAmountFilter"
          default-value="all"
          style="width: 100%"
        >
          <a-select-option value="all"> 전체 </a-select-option>
          <a-select-option value="0"> 5억 미만 </a-select-option>
          <a-select-option value="20"> 5억 이상 </a-select-option>
          <a-select-option value="30"> 10억 이상 </a-select-option>
        </a-select>
      </a-col>
    </a-row>
    <!--------------------------------- /Search Bar  --------------------------------->

    <!--------------------------------- kakao map  --------------------------------->
    <a-row :gutter="24">
      <a-col :span="24">
        <div
          style="
            width: 100%;
            height: 700px;
            margin-bottom: 30px;
            text-align: center;
          "
        >
          <strong>kakao map</strong>
          <div id="map"></div>
        </div>
      </a-col>
    </a-row>

    <!--------------------------------- /kakao map  --------------------------------->

    <a-row type="flex" :gutter="24">
      <!-- Billing Info Column -->
      <a-col :span="24" :md="16">
        <a-row type="flex" :gutter="24">
          <a-col :span="24" :xl="12" class="mb-24">
            <!-- Master Card -->
            <CardCredit></CardCredit>
            <!-- / Master Card -->
          </a-col>
          <a-col
            :span="12"
            :xl="6"
            class="mb-24"
            v-for="(salary, index) in salaries"
            :key="index"
          >
            <!-- Salary Card -->
            <WidgetSalary
              :value="salary.value"
              :prefix="salary.prefix"
              :icon="salary.icon"
              :title="salary.title"
              :content="salary.content"
            ></WidgetSalary>
            <!-- / Salary Card -->
          </a-col>
          <a-col :span="24" class="mb-24">
            <!-- Payment Methods Card -->
            <CardPaymentMethods></CardPaymentMethods>
            <!-- Payment Methods Card -->
          </a-col>
        </a-row>
      </a-col>
      <!-- / Billing Info Column -->

      <!-- Invoices Column -->
      <a-col :span="24" :md="8" class="mb-24">
        <!-- Invoices Card -->
        <CardInvoices :data="invoiceData"></CardInvoices>
        <!-- / Invoices Card -->
      </a-col>
      <!-- / Invoices Column -->
    </a-row>

    <a-row type="flex" :gutter="24">
      <!-- Billing Information Column -->
      <a-col :span="24" :md="16" class="mb-24">
        <!-- Billing Information Card -->
        <CardBillingInfo></CardBillingInfo>
        <!-- / Billing Information Card -->
      </a-col>
      <!-- Billing Information Column -->

      <!-- Your Transactions Column -->
      <a-col :span="24" :md="8" class="mb-24">
        <!-- Your Transactions Card -->
        <CardTransactions :data="transactionsData"></CardTransactions>
        <!-- / Your Transactions Card -->
      </a-col>
      <!-- / Your Transactions Column -->
    </a-row>
  </div>
</template>

<script>
import CardCredit from "../components/Cards/CardCredit";
import WidgetSalary from "../components/Widgets/WidgetSalary";
import CardPaymentMethods from "../components/Cards/CardPaymentMethods";
import CardInvoices from "../components/Cards/CardInvoices";
import CardBillingInfo from "../components/Cards/CardBillingInfo";
import CardTransactions from "../components/Cards/CardTransactions";
import http from "@/api/http";
// Salary cards data
const salaries = [
  {
    value: 2000,
    prefix: "+$",
    icon: `
										<svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 22 22">
											<g id="bank" transform="translate(0.75 0.75)">
												<path id="Shape" transform="translate(0.707 9.543)" fill="none" stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="1.5"/>
												<path id="Path" d="M10.25,0,20.5,9.19H0Z" fill="none" stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="1.5"/>
												<path id="Path-2" data-name="Path" d="M0,.707H20.5" transform="translate(0 19.793)" fill="none" stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="1.5"/>
											</g>
										</svg>`,
    title: "Salary",
    content: "Belong Interactive",
  },
  {
    value: 49000,
    prefix: "+$",
    icon: `
										<img src="images/logos/paypal-logo-2.png" alt="">`,
    title: "Paypal",
    content: "Freelance Payment",
  },
];
// "Invoices" list data.
const invoiceData = [
  {
    title: "March, 01, 2021",
    code: "#MS-415646",
    amount: "180",
  },
  {
    title: "February, 12, 2021",
    code: "#RV-126749",
    amount: "250",
  },
  {
    title: "April, 05, 2020",
    code: "#FB-212562",
    amount: "550",
  },
  {
    title: "June, 25, 2019",
    code: "#QW-103578",
    amount: "400",
  },
  {
    title: "March, 03, 2019",
    code: "#AR-803481",
    amount: "700",
  },
];
// "Your Transactions" list data.
const transactionsData = [
  {
    period: "NEWEST",
  },
  {
    title: "Netflix",
    datetime: "27 March 2021, at 12:30 PM",
    amount: "2,500",
    type: -1, // 0 is for pending, 1 is for deposit, -1 is for withdrawal.
    status: "danger",
  },
  {
    title: "Apple",
    datetime: "27 March 2021, at 04:30 AM",
    amount: "2,000",
    type: 1,
    status: "success",
  },
  {
    period: "YESTERDAY",
  },
  {
    title: "Stripe",
    datetime: "26 March 2021, at 12:30 AM",
    amount: "750",
    type: 1,
    status: "success",
  },
  {
    title: "HubSpot",
    datetime: "26 March 2021, at 11:30 AM",
    amount: "1,050",
    type: 1,
    status: "success",
  },
  {
    title: "Creative Tim",
    datetime: "26 March 2021, at 07:30 AM",
    amount: "2,400",
    type: 1,
    status: "success",
  },
  {
    title: "Webflow",
    datetime: "26 March 2021, at 04:00 AM",
    amount: "Pending",
    type: 0,
    status: "warning",
  },
];
export default {
  components: {
    CardCredit,
    WidgetSalary,
    CardPaymentMethods,
    CardInvoices,
    CardBillingInfo,
    CardTransactions,
  },
  data() {
    return {
      // Salary cards data
      salaries,
      // Associating "Invoices" list data with its corresponding property.
      invoiceData,
      // Associating "Your Transactions" list data with its corresponding property.
      transactionsData,
      map: null,
      markerPositions: [],
      markerSet: [],
      centerSetting: false,
      starbucksList: [],
      sidoList: [{ code: "default", name: "시/도 선택" }],
      sidocode: "default",
      gugunList: [{ code: "default", name: "구/군 선택" }],
      guguncode: "default",

      // filter
      areaFilter: "all",
      floorFilter: "all",
      dealAmountFilter: "all",
    };
  }, // end of data
  created() {
    this.getSidoList();
  },
  mounted() {
    if (window.kakao && window.kakao.maps) {
      this.initMap();
    } else {
      const script = document.createElement("script");
      /* global kakao */
      script.onload = () => kakao.maps.load(this.initMap);
      script.src =
        "http://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=8273ad75e4cf13f650633b14013a60c0&libraries=services";
      document.head.appendChild(script);
    }
  },
  methods: {
    initMap() {
      console.log("initMap");
      var container = document.getElementById("map"); //지도를 담을 영역의 DOM 레퍼런스
      var options = {
        //지도를 생성할 때 필요한 기본 옵션
        center: new kakao.maps.LatLng(33.450701, 126.570667), //지도의 중심좌표.
        level: 4, //지도의 레벨(확대, 축소 정도)
      };
      this.map = new kakao.maps.Map(container, options); //지도 생성 및 객체 리턴
    },
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
      http.get("/region/gugun/" + code).then(({ data }) => {
        data.forEach((element) => {
          this.gugunList.push(element);
        });
      });
    },
    gugunChange() {
      console.log("gugun change");
    },
    search: function () {
      console.log("serach button");
      console.log(
        "filter",
        this.areaFilter,
        this.floorFilter,
        this.dealAmountFilter
      );
      console.log("codes : ", this.sidocode, this.guguncode);
    },
    handleChange: function () {},
    searchLoading: function () {},
    onSearch: function () {},
    change: function () {},
  },
}; // end of export
</script>

<style lang="scss" scoped>
#map {
  width: 100%;
  height: 100%;
}
</style>
