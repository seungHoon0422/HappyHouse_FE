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
    <!-- <a-table
      :columns="columns"
      :data-source="data"
      :pagination="false"
      :rowKey="index"
    >
      <template slot="aptname" slot-scope="aptname">
        <h6 class="m-0">{{ aptname }}</h6>
      </template>
    </a-table> -->
  </a-card>
  <!-- / Conversations Card -->
</template>

<script>
import { mapState } from "vuex";

const memberStore = "memberStore";
export default {
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    columns: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {};
  },
  created() {},
  computed: {
    ...mapState(memberStore, ["userInfo"]),
  },
};
</script>
