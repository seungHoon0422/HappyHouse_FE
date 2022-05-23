<template>
  <a-card
    :bordered="false"
    class="header-solid h-full card-profile-information"
    :bodyStyle="{ paddingTop: 0, paddingBottom: '16px' }"
    :headStyle="{ paddingRight: 0 }"
    :customRow="clickrow"
  >
    <template #title>
      <h6 class="font-semibold bg-gray-3 m-0 pl-10">{{ aptname }}</h6>
      <br />
      <h10 class="font-regular text-gray-9 m-0 pl-10">{{
        sidodetail.sidoName +
        " " +
        sidodetail.gugunName +
        " " +
        sidodetail.dongName
      }}</h10>
    </template>
    <br />
    <a-table :columns="columns" :data-source="data" :pagination="false">
    </a-table>
  </a-card>
</template>

<script>
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
      type: Array,
      default: "",
    },
    columns: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      detailInterest: [],
    };
  },
  watch: {
    data: function (newData, oldData) {
      this.detailInterest = newData;
    },
    data: function (newData, oldData) {
      this.sidodetail = newData;
    },
  },
  methods: {
    clickrow: function (record, index) {
      return {
        on: {
          click: () => {
            console.log(this.aptname);
          },
        },
      };
    },
  },
};
</script>

<style></style>
