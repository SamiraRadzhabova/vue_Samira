<template>
  <div class="wrapper">
    <div class="sample">
      <form>
        <div class="progress">
          <div
            class="progress-bar"
            role="progressbar"
            :style="progressStyles"
          ></div>
        </div>
        <div>
          <input-app
            v-for="(input, index) in info"
            :key="input.name"
            :label="input.name"
            :value="input.value"
            :valid="input.valid"
            @inp="onInput($event, index)"
          ></input-app>
        </div>

        <button class="btn btn-primary" :disabled="!formReady">
          Send Data
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import InputApp from "./components/InputApp.vue";

export default {
  name: "App",
  components: {
    InputApp,
  },
  data: () => ({
    info: [
      {
        name: "Name",
        value: "",
        pattern: /^[a-zA-Z ]{2,30}$/,
      },
      {
        name: "Phone",
        value: "",
        pattern: /^[0-9]{7,14}$/,
      },
      {
        name: "Email",
        value: "",
        pattern: /.+/,
      },
      {
        name: "Some Field 1",
        value: "",
        pattern: /.+/,
      },
      {
        name: "Some Field 2",
        value: "",
        pattern: /.+/,
      },
    ],
  }),
  computed: {
    fieldDone() {
      return this.info.reduce((total, field) => {
        return total + (field.valid ? 1 : 0);
      }, 0);
    },
    formReady() {
      return this.fieldDone === this.info.length;
    },
    progressStyles() {
      return {
        width: (this.fieldDone / this.info.length) * 100 + "%",
      };
    },
  },
  created() {
    this.info.forEach((field) => {
      field.valid = false;
    });
  },
  methods: {
    onInput(value, i) {
      let field = this.info[i];
      field.value = value.trim();
      field.valid = field.pattern.test(value);
    },
  },
};
</script>

<style>
@import "~bootstrap/dist/css/bootstrap.css";
body {
  width: 1000px;
  margin-left: 300px;
  margin-top: 50px;
}
</style>
