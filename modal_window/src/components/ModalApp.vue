<template>
<div class="container">
  <div class="model">
    <div class="model-up">
      <a class="but" @click="showMd">&#10006;</a>
    </div>
    <slot></slot>
  </div></div>
</template>

<script>
export default {
  name: "App",
  components: {
    name: "ModalApp",
  },
    methods: {
    showMd(){
      this.$emit('close-window');
    }
  },
};
</script>

<style>
.model {
  width: 700px;
  height: 500px;
  background-color: #ECEFF1;
  box-shadow: 6px 6px 20px rgba(0, 0, 0, 0.3);
  margin-top: 20px;
  margin-left: 350px;
}
.model-up {
  width: 700px;
  height: 60px;
  background-color:  #546E7A;
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
