<template>
  <main id="todolist">
    <h1>
      Todo List
      <span>Today i need To :</span>
    </h1>
    <app-tag
      title="Всё"
      :class="{ active: !activeTab }"
      @but-click="changeTab(null)"
    ></app-tag>
    <app-tag
      v-for="butt in tagList"
      :key="butt"
      :class="{ active: activeTab === butt.content }"
      :title="butt.content"
      @but-click="changeTab(butt.content)"
    ></app-tag>
    <transition-group name="todolist" tag="ul" v-if="defaultData?.length">
      <app-task
        :class="{ done: task.done }"
        v-for="(task, i) in filteredTabs"
        :key="task.description + i"
        :description="task.description"
        :tag="task.tag"
        @check-task="handleCheck(i)"
        @delete-task="deleteTask(i)"
        @edit-task="editTask(i)"
      ></app-task>
    </transition-group>
    <p class="emptylist" v-else>Your todo list is empty.</p>
    <div
      class="togglebutton-wrapper"
      :class="sortActive ? 'togglebutton-checked' : ''"
    >
      <label for="name">
        <span class="togglebutton-label">Sort</span>
        <span class="tooglebutton-box"></span>
      </label>
      <input type="checkbox" id="name" v-model="sortActive" />
    </div>
    <form name="newform">
      <label for="newitem">Add to the todo list</label>
      <input type="text" name="newitem" id="newitem" v-model="currentTask" />
      <select name="" v-model="selectedTag">
        <option v-for="tag in tagList" :value="tag" :key="tag.id">
          {{ tag.content }}
        </option></select
      ><button type="button" @click="editMode ? saveChanges() : addNewTask()">
        {{ editMode ? "Save changes" : "Add item" }}
      </button>
    </form>
  </main>
</template>

<script>
import AppTag from "./components/AppTag.vue";
import AppTask from "./components/AppTask.vue";
export default {
  name: "App",
  components: {
    AppTask,
    AppTag,
  },
  data: () => ({
    defaultData: [
      {
        description: "Подготовить шаблон компонента",
        tag: {
          id: 1,
          content: "Работа",
        },
        done: false,
      },
      {
        description: "Позвонить и договориться о встрече",
        tag: {
          id: 0,
          content: "Личное",
        },
        done: false,
      },
      {
        description: "js",
        tag: {
          id: 3,
          content: "Учеба",
        },
        done: false,
      },
      {
        description: "Сходить на тренировку",
        tag: {
          id: 2,
          content: "Спорт",
        },
        done: false,
      },
      {
        description: "Предложить сыграть в какую-то стратежку",
        tag: {
          id: 4,
          content: "Досуг",
        },
        done: false,
      },
    ],
    tagList: [
      {
        id: 1,
        content: "Работа",
      },
      {
        id: 0,
        content: "Личное",
      },
      {
        id: 3,
        content: "Учеба",
      },
      {
        id: 2,
        content: "Спорт",
      },
      {
        id: 4,
        content: "Досуг",
      },
    ],
    selectedTag: null,
    currentTask: null,
    editMode: false,
    activaTask: null,
    sortActive: false,
    activeTab: null,
  }),
  watch: {
    sortActive() {
      this.sortByDone();
    },
  },
  created() {
    if (localStorage.getItem("data")) {
      this.defaultData = JSON.parse(localStorage.getItem("data"));
    }
  },
  computed: {
    filteredTabs() {
      return this.defaultData.filter(
        (item) => !this.activeTab || item.tag.content.includes(this.activeTab)
      );
    },
  },
  methods: {
    handleCheck(i) {
      this.defaultData[i].done = !this.defaultData[i].done;
    },
    addNewTask() {
      this.defaultData.push({
        description: this.currentTask,
        tag: this.selectedTag,
        done: false,
      });
      this.saveData();
    },
    deleteTask(i) {
      this.defaultData.splice(i, 1);
      this.saveData();
    },
    saveData() {
      this.defaultData.length
        ? localStorage.setItem("data", JSON.stringify(this.defaultData))
        : localStorage.removeItem("data");
    },
    editTask(i) {
      this.editMode = !this.editMode;
      this.activaTask = i;
      this.currentTask = this.defaultData[i].description;
      this.selectedTag = this.defaultData[i].tag;
    },
    saveChanges() {
      this.editMode = false;
      this.defaultData[this.activaTask].description = this.currentTask;
      this.defaultData[this.activaTask].tag = this.selectedTag;
      this.saveData();
      this.currentTask = null;
      this.selectedTag = null;
    },
    sortByDone() {
      this.defaultData.sort((a, b) => {
        return this.sortActive ? a.done - b.done : b.done - a.done;
      });
    },
    changeTab(tab) {
      this.activeTab = tab;
    },
  },
};
</script>

<style>
#todolist .todolist-move {
  transition: transform 1s;
}
#todolist {
  margin: 4rem auto;
  padding: 2rem 3rem 3rem;
  max-width: 500px;
  background: #67a4ab;
  color: #fff;
  box-shadow: -20px -20px 0px 0px rgba(100, 100, 100, 0.1);
}
#todolist h1 {
  /*text-align:center;*/
  font-weight: normal;
  font-size: 2.6rem;
  letter-spacing: 0.05em;
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
}
#todolist h1 span {
  display: block;
  font-size: 0.8rem;
  margin-bottom: 0.7rem;
  margin-left: 3px;
  margin-top: 0.2rem;
}

#todolist .emptylist {
  margin-top: 2.6rem;
  text-align: center;
  letter-spacing: 0.05em;
  font-style: italic;
  opacity: 0.8;
}
#todolist ul {
  margin-top: 2.6rem;
  list-style: none;
}
form {
  margin-top: 3rem;
  display: flex;
  flex-wrap: wrap;
}
form label {
  min-width: 100%;
  margin-bottom: 0.5rem;
  font-size: 1.3rem;
}
form input {
  flex-grow: 1;
  border: none;
  background: #f7f1f1;
  padding: 0 1.5em;
  font-size: initial;
}
form button {
  padding: 0 1.3rem;
  border: none;
  background: #ff6666;
  color: white;
  text-transform: uppercase;
  font-weight: bold;
  border: 1px solid rgba(255, 255, 255, 0.3);
  margin-left: 5px;
  cursor: pointer;
  transition: background 0.2s ease-out;
}
form button:hover {
  background: #ff5e5e;
}
form input,
form button {
  font-family: "Quicksand", sans-serif;
  height: 3rem;
}
.togglebutton-wrapper {
  margin-top: 1em;
}
.togglebutton-wrapper label {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
.togglebutton-wrapper input {
  position: absolute;
  left: -9999px;
}
.togglebutton-wrapper .togglebutton-label {
  font-size: 0.8rem;
  letter-spacing: 0.1em;
}
.togglebutton-wrapper .tooglebutton-box {
  position: relative;
  display: block;
  margin-left: 0.6em;
  width: 38px;
  height: 22px;
  background: white;
  /*border:1px solid black;*/
  border-radius: 999px;
  cursor: pointer;
}
.togglebutton-wrapper .tooglebutton-box:before {
  content: "";
  position: absolute;
  top: 2px;
  left: 2px;
  display: block;
  width: 18px;
  height: 18px;
  /*border:1px solid #FF6666;*/
  border-radius: 50%;
  background: #ff6666;
  opacity: 0.7;
  transition: all 0.2s ease-in-out;
}
.togglebutton-wrapper.togglebutton-focus .tooglebutton-box {
  box-shadow: 0px 0px 0px 3px rgba(0, 0, 0, 0.1);
}
.togglebutton-wrapper.togglebutton-checked .tooglebutton-box:before {
  left: calc(100% - 4px - 16px);
  opacity: 1;
}
</style>
