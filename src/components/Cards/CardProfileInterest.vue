<template>
  <!-- Conversations Card -->
  <a-card
    :bordered="false"
    class="header-solid h-full card-profile-information"
    :bodyStyle="{ paddingTop: 0, paddingBottom: '16px' }"
    :headStyle="{ paddingRight: 0 }"
  >
    <!-- <template #title>
      <h6 class="font-semibold m-0 pl-10">나의 관심목록</h6> -->
    <!-- </template>
    <template>
      <a-list item-layout="horizontal" :data-source="data">
        <template #renderItem="{ item }">
          <a-list-item>
            <a-list-item-meta>
              <template #title>
                <a href="https://www.antdv.com/">{{ item.title }}</a>
              </template>
            </a-list-item-meta>
          </a-list-item>
        </template>
      </a-list>
    </template> -->

    <!-- <a-table :columns="columns" :data-source="data" :pagination="false">
      <template>
        <h6 class="m-0">{{ data.title }}</h6>
      </template>
    </a-table> -->
    <h2>{{ data }}</h2>
    <a-table
      :columns="columns"
      :data-source="data"
      :pagination="false"
      :ow-key="key"
    >
      <template slot="title" slot-scope="title">
        <div class="table-avatar-info">
          <div class="avatar-info">
            <h6>{{ title }}</h6>
          </div>
        </div>
      </template>
    </a-table>
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
