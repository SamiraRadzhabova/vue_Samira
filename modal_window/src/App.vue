<template>
  <div class="container">
    <a href="" class="btn" @click="showWindow">CLICK ME</a>
    <modal-app :shows="showModal" v-if="showModal" @close-window="showWindow">
      <h1 class="info">Black Panther: Wakanda Forever</h1>
      <img src="@/assets/black_pantera.jpg" alt="" class="img-film" />
    </modal-app>
  </div>
</template>

<script>
import ModalApp from "./components/ModalApp.vue";

export default {
  name: "App",
  components: {
    ModalApp,
  },
  data() {
    return {
      showModal: true,
    };
  },
  mounted() {
    document.addEventListener("click", this.showWindow.bind(this), true);
  },
  unmounted() {
    document.removeEventListener("click", this.showWindow.bind(this), true);
  },
  methods: {
    showWindow() {
      this.showModal = !this.showModal;
    },
  },
};
</script>

<style>
.container {
  width: 1200px;
  margin-left: auto;
  margin-right: auto;
}

.btn {
  display: block;
  position: absolute;
  width: 300px;
  height: 30px;
  border: 3px solid #263852;
  font-size: 20px;
  text-transform: uppercase;
  font-weight: bold;
  text-align: center;
  color: #263852;
  text-decoration: none;
  border-radius: 3px;
  color: #263852;
  position: relative;
  transition: 0.5s;
  overflow: hidden;
  padding-top: 15px;
  padding-bottom: 10px;
  margin-left: 450px;
  margin-top: 50px;
}
.btn::before,
.butt::after {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  background: #263852;
  top: 0;
  left: -100%;
  transition: 0.3s;
  z-index: -1;
}
.btn::after {
  opacity: 1;
  transition-delay: 0.1s;
}
.btn:hover {
  color: #fff;
}
.btn:hover::before,
.butt:hover::after {
  left: 0;
}
.img-film {
  width: 300px;
  height: 400px;
  padding-left: 20px;
  padding-top: 20px;
  padding-left: 200px;
}
.info {
  padding-left: 120px;
}
</style>
