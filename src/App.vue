<template>
  <div id="app">
    <TreeList :treeData="treeData"></TreeList>
  </div>
</template>

<script>
import TreeList from "@/components/TreeList.vue";
export default {
  name: "app",
  components: {
    TreeList
  },
  data() {
    return {
      treeData: {
        name: "My Tree",
        children: [
          { name: "hello" },
          { name: "wat" },
          {
            name: "child folder",
            children: [
              {
                name: "child folder",
                children: [{ name: "hello" }, { name: "wat" }]
              },
              { name: "hello" },
              { name: "wat" },
              {
                name: "child folder",
                children: [{ name: "hello" }, { name: "wat" }]
              }
            ]
          }
        ]
      }
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.bold {
  font-weight: bold;
}

.itemAction {
  margin-left: 5px;
}
</style>
