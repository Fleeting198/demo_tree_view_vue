<template>
  <div class="editableLabel">
    <input
      class="textInput"
      type="text"
      v-if="isEditing"
      :value="value"
      @change="$emit('change', $event.target.value)"
      @keydown.enter="isEditing=false"
    />
    <span class="textLabel" v-if="!isEditing">{{value}}</span>
    <span class="itemAction" @click="toggle">[ e ]</span>
  </div>
</template>

<script>
export default {
  name: "EditableLabel",
  props: {
    value: String
  },
  data() {
    return {
      isEditing: false
    };
  },
  methods: {
    toggle() {
      this.isEditing = !this.isEditing;
    }
  }
};
</script>

<style scoped>
.editableLabel {
  display: inline-block;
}
.textInput {
}
.textLabel {
}
</style>