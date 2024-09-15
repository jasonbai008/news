<template>
  <div class="list-wrap">
    <div class="item" v-for="(n, i) in listData" :key="i">
      <span>{{ n.index }}.</span>
      <a :href="n.url" class="title" target="_blank">{{ n.title }}</a>
    </div>
    <p>{{ updateDate }}</p>
  </div>
</template>

<script>
export default {
  name: "list",
  props: {
    listData: {
      type: Array,
    },
    updateDate: String,
  },
  data() {
    return {};
  },
};
</script>

<style scoped lang="scss">
.list-wrap {
  height: calc(97vh - 54px);
  overflow-y: auto;
}
.item {
  text-align: left;
  margin-bottom: 20px;
  display: flex;
  align-items: baseline;
  span {
    display: inline-block;
    margin-right: 7px;
    width: 26px;
    text-align: right;
    flex-shrink: 0;
    font-size: 22px;
    font-style: italic;
    color: #555;
  }
  a {
    color: #409eff;
    padding-right: 12px;
    text-align: justify;
    line-height: 25px;
    text-decoration: none;
    letter-spacing: 1px;
  }
}
p {
  border-top: 1px dashed #bbb;
  padding-top: 20px;
  color: #666;
}
</style>
