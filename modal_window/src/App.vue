<template>
  
    <button class="btn" @click="showWindow">CLICK ME</button>
   
    <modal-app v-if="showModal" @close-window="showWindow"> <div class="modal-backdrop">
      <div class="wrapper">
        <img src="@/assets/black_pantera.jpg" alt="" class="img-film" />
        <div>
          <h1 class="info">Black Panther: Wakanda Forever</h1>
          <p class="text">
            Black Panther is a 2018 American superhero film based on the comic
            book by Stan Lee and Jack Kirby about the character of the same name
            published by Marvel Comics. Produced by Marvel Studios and
            distributed by Walt Disney Studios Motion Pictures, the film is the
            eighteenth film in the Marvel Cinematic Universe.
          </p>
        </div>
      </div></div>
    </modal-app>
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
      showModal: false,
    };
  },
  // mounted() {
  //   document.addEventListener("click", this.showWindow.bind(this), true);
  // },
  // unmounted() {
  //   document.removeEventListener("click", this.showWindow.bind(this), true);
  // },
  methods: {
    showWindow() {
      this.showModal = !this.showModal;
    },
  },
};
</script>

<style>
body{
  background: linear-gradient(45deg,#B06AB3,#4568DC );
}
.btn {
  display: block;
  width: 150px;
  height: 40px;
  border: 1px solid #fff;
  font-size: 16px;
  padding-top: 10px;
  padding-bottom: 10px;
  text-align: center;
  color: #fff;
   background: transparent;
  border-radius: 45px;
  cursor: pointer;
  margin-left: 630px;
  margin-top: 30px;
}
/* .modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
} */
.wrapper {
  display: flex;
}
.img-film {
  width: 300px;
  height: 400px;
  margin-left: 20px;
  margin-top: 20px;
}
.info {
  margin-left: 30px;
  text-align: center;
  width: 300px;
}
.text{
  margin-left: 30px;
  font-size: 15px;
  width: 300px;
  text-align: justify;
  margin-top: 30px;
}

</style>
