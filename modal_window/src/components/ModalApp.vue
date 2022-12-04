<template>
  <div class="model" v-if="shows">
    <div class="model-up">
      <a class="but" @click="showMd"><img src="@/assets/close.png" alt="" /></a>
    </div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    name: "ModalApp",
  },
  props:{
    shows:{
      type: Boolean,
      required: true,
    }
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
  position: fixed;
  width: 700px;
  height: 600px;
  background-color: rgb(255, 255, 255);
  box-shadow: 6px 6px 20px rgba(0, 0, 0, 0.3);
  margin-left: 250px;
}
.model-up {
  width: 700px;
  height: 60px;
  background-color: rgb(0, 0, 0);
}
.but {
  padding-right: 25px;
  padding-top: 5px;
  float: right;
  cursor: pointer;
}

</style>
