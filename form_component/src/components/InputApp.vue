<template>
  <div class="form-group">
    <label>{{ label }}</label>
    <transition name="no-mode-fade" mode="out-in">
      <img class="icon" v-if="activated" :src="iconPath" alt="icon" />
    </transition>
    <input type="text" class="form-control" :value="value" @input="onInput" />
  </div>
</template>

<script>
export default {
  name: "InputApp",
  props: {
    label: {
      type: String,
      required: true,
    },
    valid: {
      type: Boolean,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      activated: false,
    };
  },
  computed: {
    iconPath() {
      return this.valid
        ? require("@/assets/yes.jpg")
        : require("@/assets/no.jpg");
    },
  },
  methods: {
    onInput(e) {
      this.activated = true;
      this.$emit("inp", e.target.value);
    },
  },
};
</script>

<style>
.no-mode-fade-enter-active,
.no-mode-fade-leave-active {
  transition: opacity 4.5s;
  }

.no-mode-fade-enter-from,
.no-mode-fade-leave-to {
  opacity: 0;
}
.icon {
  width: 3%;
}
</style>
