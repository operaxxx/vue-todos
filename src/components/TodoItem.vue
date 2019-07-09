<template>
  <li>
    <Checkbox v-model="isChecked"></Checkbox>
    <slot name="todoContent" v-bind="{isChecked}"></slot>
    <a href="#" style="margin-left:20px" @click="$emit('remove')">
      <Icon type="md-close" />
    </a>
  </li>
</template>

<script>
export default {
  props: {
    todo: {},
    index: {}
  },
  data() {
    return {
      isChecked: false
    };
  }
};
</script>

<style scoped>
li {
  padding-bottom: 4px;
}
</style>
