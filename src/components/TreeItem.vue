<template>
  <li class="treeItem">
    <!--  -->
    <div :class="{bold:isFolder}" @click="toggle" @dblclick="makeFolder">
      <EditableLabel :value="item.name" @change="handleNameChange" />
      <span @click="deleteItem" class="itemAction">[ x ]</span>
      <span v-if="isFolder" class="itemAction">[ {{ isOpen?'-':'+' }} ]</span>
    </div>

    <!--  -->
    <ul v-if="isFolder" v-show="isOpen">
      <!--  -->
      <TreeItem
        v-for="(child) in item.children"
        :key="getKeyOfChildItem(child)"
        :item="child"
        @makeFolder="handleMakeFolder"
        @addItem="handleAddItem"
        @deleteItem="handleDeleteItem"
      ></TreeItem>

      <!--  -->
      <li @click="addItem">[ + ]</li>
    </ul>
  </li>
</template>

<script>
import EditableLabel from "@/common/EditableLabel";
import { truncate } from "fs";
export default {
  name: "TreeItem",
  components: {
    EditableLabel
  },
  props: {
    item: Object
  },
  data() {
    return {
      isOpen: false,
      childrenKeys: new Map()
    };
  },
  computed: {
    isFolder() {
      return this.item.children && this.item.children.length;
    }
  },
  methods: {
    toggle() {
      if (this.isFolder) {
        this.isOpen = !this.isOpen;
      }
    },
    getKeyOfChildItem(item) {
      let key = this.childrenKeys.get(item);
      if (key !== undefined) {
        return key;
      } else {
        key = Math.random().toFixed(8);
        this.childrenKeys.set(item, key);
      }
    },
    addItem() {
      this.$emit("addItem", this.item);
    },
    handleAddItem(e) {
      this.$emit("addItem", e);
    },
    makeFolder() {
      if (!this.isFolder) {
        this.$emit("makeFolder", this.item);
        this.isOpen = true;
      }
    },
    handleMakeFolder(e) {
      this.$emit("makeFolder", e);
    },
    deleteItem() {
      this.$emit("deleteItem", this.item);
    },
    handleDeleteItem(itemTarget) {
      for (let i = 0; i < this.isFolder; i++) {
        const child = this.item.children[i];
        if (
          child.name === itemTarget.name &&
          child.children === itemTarget.children
        ) {
          this.item.children.splice(i, 1);
          break;
        }
      }
    },
    handleNameChange(value) {
      this.item.name = value;
    }
  }
};
</script>

<style scoped>
</style>
