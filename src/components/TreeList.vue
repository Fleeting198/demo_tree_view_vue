<template>
  <ul class="treeList">
    <!-- 根结点没有注册deleteItem回调, 所以尽管删除元素的按钮存在, 点击按钮时无事发生 -->
    <TreeItem :item="treeData" @addItem="addItem" @makeFolder="makeFolder"></TreeItem>
  </ul>
</template>

<script>
import TreeItem from "@/components/TreeItem.vue";
export default {
  name: "TreeList",
  components: {
    TreeItem
  },
  props: {
    treeData: Object
  },
  methods: {
    makeFolder(item) {
      this.$set(item, "children", []);
      this.addItem(item);
    },
    addItem(item) {
      item.children.push({ name: "new item" });
    }
  }
};
</script>

<style>
.treeList {
  user-select: none;
}
</style>
