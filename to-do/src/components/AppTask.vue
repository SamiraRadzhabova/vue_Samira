<template>
  <li>
    <div class="wrapper">
      <span class="label">{{ description }}</span>
      <div class="actions">
        <button
          class="btn-picto"
          type="button"
          aria-label="Delete"
          title="Delete"
        >
          <img src="@/assets/icons/checkbox-icon.svg" alt="" @click="onCheck" />
        </button>
        <button class="btn-picto" type="button" @click="onEdit">
          <img src="@/assets/icons/task-edit-icon.svg" alt="edit" />
        </button>
        <button
          class="btn-picto"
          type="button"
          aria-label="Delete"
          title="Delete"
          @click="onDelete"
        >
          <img src="@/assets/icons/delete-icon.svg" alt="delete" />
        </button>
      </div>
    </div>
    <div class="tag" :style="tagColor">{{ tag.content }}</div>
  </li>
</template>
<script>
export default {
  name: "AppTask",
  props: {
    description: {
      type: String,
      required: true,
    },
    tag: {
      type: Object,
      required: true,
    },
  },
  data: () => ({
    colors: [
      {
        id: 0,
        value: "#cb3c3c",
      },
      {
        id: 1,
        value: "#79ba63",
      },
      {
        id: 2,
        value: "#8f18a2",
      },
      {
        id: 3,
        value: "#a1ad44",
      },
      {
        id: 4,
        value: "#6a615e",
      },
    ],
  }),
  computed: {
    tagColor() {
      return {
        backgroundColor: this.colors.find((obj) => obj.id === this.tag.id)
          .value,
      };
    },
  },
  methods: {
    onCheck() {
      this.$emit("check-task");
    },
    onEdit() {
      this.$emit("edit-task");
    },
    onDelete() {
      this.$emit("delete-task");
    },
  },
};
</script>

<style>
@keyframes strikeitem {
  to {
    width: calc(100% + 1rem);
  }
}
.wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  width: 100%;
}
.tag {
  margin-top: 10px;
  display: flex;
  padding: 5px;
  border-radius: 8px;
}

#todolist li {
  display: flex;
  flex-direction: column;
  margin: 0 -3rem 4px;
  padding: 1.1rem 3rem;
  justify-content: space-between;
  align-items: flex-start;
  background: rgba(255, 255, 255, 0.1);
}

#todolist .actions {
  flex-shrink: 0;
  padding-left: 0.7em;
  display: flex;
  align-items: center;
  gap: 5px;
}
#todolist .label {
  position: relative;
  transition: opacity 0.2s linear;
}
#todolist .done .label {
  opacity: 0.6;
}
#todolist .done .label:before {
  content: "";
  position: absolute;
  top: 50%;
  left: -0.5rem;
  display: block;
  width: 0%;
  height: 3px;
  background: #fff;
  animation: strikeitem 0.3s ease-out 0s forwards;
}
#todolist .btn-picto {
  border: none;
  background: none;
  -webkit-appearance: none;
  cursor: pointer;
  color: #fff;
  width: 32px;
  height: 32px;
  padding: 0;
}
#todolist .btn-picto img {
  height: 100%;
  width: 100%;
}
</style>
