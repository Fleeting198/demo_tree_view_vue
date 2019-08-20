<template>
  <div class="editableLabel">
    <input
      class="textInput"
      type="text"
      ref="input"
      v-if="isEditing"
      :value="value"
      @change="$emit('change', $event.target.value)"
      @keydown.enter="isEditing=false"
      @blur="endEdit"
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
    startEdit() {
      this.isEditing = true;
      this.$nextTick(function() {
        this.$refs.input.focus();
      });
    },
    endEdit() {
      this.isEditing = false;
    },
    toggle() {
      if (this.isEditing) {
        this.endEdit();
      } else {
        this.startEdit();
      }
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