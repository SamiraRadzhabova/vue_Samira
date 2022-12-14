<template>
  <button class="but" @click="handleClick">{{ title }}</button>
</template>

<script>
export default {
  name: "AppTag",
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleClick() {
      this.$emit("but-click");
    },
  },
};
</script>

<style scoped>
.but {
  width: 70px;
  min-height: 30px;
  margin-right: 5px;
  border-radius: 15px;
  border: 1px solid #fff;
  cursor: pointer;
  background: transparent;
  color: #fff;
  font-size: 15px;
}
.active {
  background-color: #4e777b;
}
</style>
