<template>
  <div>
    <a-row :gutter="24">
      <a-col :span="12" style="padding: 20px">
        <a-card
          :bordered="false"
          class="header-solid"
          :bodyStyle="{ padding: 0 }"
        >
          <template #title>
            <a-row type="flex" align="middle">
              <a-col :span="24" :md="12">
                <h5 class="font-semibold m-0">매매 목록</h5>
              </a-col>
            </a-row>
          </template>
          <a-table :columns="columns" :data-source="data" :pagination="true">
            <template slot="no" slot-scope="no">
              <div class="author-info">
                <h6 class="m-0">{{ no }}</h6>
              </div>
            </template>

            <template slot="aptName" slot-scope="aptName">
              <div class="table-avatar-info">
                <!-- <a-avatar shape="square" :src="author.avatar" /> -->
                <div class="avatar-info">
                  <h6>{{ aptName }}</h6>
                  <!-- <p>{{ userid }}</p> -->
                </div>
              </div>
            </template>
            <template slot="dealAmount" slot-scope="dealAmount">
              <div class="table-avatar-info">
                <!-- <a-avatar shape="square" :src="author.avatar" /> -->
                <div class="avatar-info">
                  <h6>{{ dealAmount }}</h6>
                  <!-- <p>{{ userid }}</p> -->
                </div>
              </div>
            </template>
          </a-table>
        </a-card>
      </a-col>
      <a-col :span="12"> 매매 상세페이지 </a-col>
    </a-row>
  </div>
</template>

<script>
export default {
  name: "MuseVueAntDesignDashboardMainDrawHouseTable",

  props: ["data"],
  data() {
    return {
      columns: [
        {
          title: "거래번호",
          dataIndex: "no",
          scopedSlots: { customRender: "no" },
        },
        {
          title: "아파트 이름",
          dataIndex: "aptName",
          scopedSlots: { customRender: "aptName" },
        },
        {
          title: "매매가격",
          dataIndex: "dealAmount",
          scopedSlots: { customRender: "dealAmount" },
        },
      ],
    };
  },

  created() {},
  mounted() {
    console.log("table items ", this.$props.data);
  },

  methods: {},
};
</script>

<style lang="scss" scoped></style>
