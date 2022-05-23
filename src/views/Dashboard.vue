<!-- 
	This is the dashboard page, it uses the dashboard layout in: 
	"./layouts/Dashboard.vue" .
 -->

<template>
  <div
    style="
      position: absolute;
      top: 0;
      width: 100%;
      height: 100vh;
      background: url(https://photo.coolenjoy.net/data/editor/2108/2117eaf4086e95f302f5fdcc3dd04c979011f6e2.jpg)
        no-repeat center;
      background-size: 100%;
    "
  >
    <!--setting main dashboard-->

    <a-row style="text-align: center; justify-content: center">
      <a-row class="bg">
        <a-col :span="24">
          <div
            style="
              color: antiquewhite;
              position: relative;
              margin-top: 10%;
              font-size: xx-large;
            "
          >
            HAPPY HOUSE
          </div>

          <div
            style="
              width: 200px;
              position: relative;
              margin-top: 15%;
              margin-left: auto;
              margin-right: auto;
            "
          >
            <router-link to="/billing">
              <a-button shape="round" block class="bolder">Find House</a-button>
            </router-link>
          </div>
        </a-col>
        <a-row :gutter="24" type="flex">
          <a-col :span="6"></a-col>
          <a-col :span="6">
            <div>
              <a-row>
                <a-card
                  title="공지사항"
                  :bordered="true"
                  style="margin-top: 30%; margin-left: auto; margin-right: auto"
                  :size="small"
                >
                  <template #extra><a href="#/tables">more</a></template>
                  <a-table
                    :dataSource="articleItems"
                    :columns="columns"
                    :pagination="false"
                    :size="small"
                  />
                </a-card>
              </a-row>
            </div>
          </a-col>
          <a-col :span="6">
            <div>
              <a-row>
                <a-card
                  title="NEWS"
                  :bordered="true"
                  style="margin-top: 30%; margin-left: auto; margin-right: auto"
                  :size="small"
                >
                  <template #extra><a href="#/tables">more</a></template>
                  <a-table
                    :dataSource="articleItems"
                    :columns="columns"
                    :pagination="false"
                    :size="small"
                  />
                </a-card>
              </a-row>
            </div>
          </a-col>
          <a-col :span="6"></a-col>
        </a-row>
      </a-row>
    </a-row>

    <!-- <a-row :gutter="24">
      <a-col
        :span="24"
        :lg="12"
        :xl="6"
        class="mb-24"
        v-for="(stat, index) in stats"
        :key="index"
      >
        <WidgetCounter
          :title="stat.title"
          :value="stat.value"
          :prefix="stat.prefix"
          :suffix="stat.suffix"
          :icon="stat.icon"
          :status="stat.status"
        ></WidgetCounter>
      </a-col>
    </a-row> -->

    <!-- Charts -->
    <!-- <a-row :gutter="24" type="flex" align="stretch">
      <a-col :span="24" :lg="10" class="mb-24">
        <CardBarChart></CardBarChart>
      </a-col>
      <a-col :span="24" :lg="14" class="mb-24">
        <CardLineChart></CardLineChart>
      </a-col>
    </a-row> -->
    <!-- / Charts -->

    <!-- Table & Timeline -->
    <!-- <a-row :gutter="24" type="flex" align="stretch">
      <a-col :span="24" :lg="16" class="mb-24">
        <CardProjectTable
          :data="tableData"
          :columns="tableColumns"
        ></CardProjectTable>
      </a-col>

      <a-col :span="24" :lg="8" class="mb-24">
        <CardOrderHistory></CardOrderHistory>
      </a-col>
    </a-row> -->
    <!-- / Table & Timeline -->

    <!-- Cards -->
    <!-- <a-row :gutter="24" type="flex" align="stretch">
      <a-col :span="24" :xl="14" class="mb-24">
        <CardInfo></CardInfo>
      </a-col>
      <a-col :span="24" :xl="10" class="mb-24">
        <CardInfo2></CardInfo2>
      </a-col>
    </a-row> -->
  </div>
</template>

<script>
// Bar chart for "Active Users" card.
import CardBarChart from "../components/Cards/CardBarChart";

// Line chart for "Sales Overview" card.
import CardLineChart from "../components/Cards/CardLineChart";

// Counter Widgets
import WidgetCounter from "../components/Widgets/WidgetCounter";

// "Projects" table component.
import CardProjectTable from "../components/Cards/CardProjectTable";

// Order History card component.
import CardOrderHistory from "../components/Cards/CardOrderHistory";

// Information card 1.
import CardInfo from "../components/Cards/CardInfo";

// Information card 2.
import CardInfo2 from "../components/Cards/CardInfo2";
import http from "@/api/http";
export default {
  components: {
    CardBarChart,
    CardLineChart,
    WidgetCounter,
    CardProjectTable,
    CardOrderHistory,
    CardInfo,
    CardInfo2,
  },
  data() {
    return {
      articleItems: [],

      columns: [
        {
          title: "no",
          dataIndex: "articleno",
          key: "articleno",
        },
        {
          title: "subject",
          dataIndex: "subject",
          key: "subject",
        },
      ],
    };
  },
  created() {
    http.get("/board").then(({ data }) => {
      this.articleItems = data.sort((a, b) => {
        return b.articleno - a.articleno;
      });
      this.articleItems = this.articleItems.splice(0, 3);
      console.log(this.articleItems);
    });
  },
};
</script>

<style lang="scss" scoped>
.bg {
  background-color: rgba(0, 0, 0, 0.5); /*살짝 투명한 검정으로 배경색*/
  width: 102%;
  height: 100vh;
  position: absolute; /*다른 요소들 위로 겹쳐질 수 있게함*/
  top: 0;
}
section {
  background-size: cover;
  display: block;
  width: 100%;
  height: 400px;
  color: #ffffff;
  text-align: center;
  padding-top: 150px;
}
section h1 {
  font-size: 2.5em;
}
section p {
  margin-bottom: 30px;
}
section h1,
p,
a {
  position: relative;
  z-index: 1000; /*맨 앞으로 나오도록 함*/
}
</style>
