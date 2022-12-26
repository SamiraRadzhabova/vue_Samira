<template>
  <div class="container" ref="modalWrapper">
    <div class="model">
      <div class="model-up">
        <a class="but" @click="showMd">&#10006;</a>
      </div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    name: "ModalApp",
  },
  mounted() {
    let refThis = this;
    document.addEventListener("click", function (item) {
      if (item.target === refThis.$refs.modalWrapper) {
        refThis.showMd();
      }
    });
  },
  methods: {
    showMd() {
      this.$emit("close-window");
    },
  },
};
</script>

<style>
.container {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
}
.model {
  width: 700px;
  height: 500px;
  background-color: #eceff1;
  box-shadow: 6px 6px 20px rgba(0, 0, 0, 0.3);
  margin-left: 350px;
  margin-top: 110px;
}
.model-up {
  width: 700px;
  height: 60px;
  background-color: #546e7a;
}
.but {
  padding-right: 25px;
  padding-top: 18px;
  float: right;
  cursor: pointer;
  color: white;
  font-size: 18px;
}
</style>
