<template>
  <div class="container mt-4">
    <h1 id="task_details">Task Details</h1><br />
    <div>
      <button :disabled="formDisabled" @click="toggleForm" id="add">Add Task</button>
      <button :disabled="storyDisabled" @click="toggleStoryList" id="story">Story List</button>
      <button :disabled="bugDisabled" @click="toggleBugList" id="bug">Bug List</button>
    </div>
    <story-list v-show="showStoryList" />
    <bug-list v-show="showBugList" />
    <FormComponent v-show="showForm" />
  </div>

</template>

<script>
import FormComponent from './components/FormComponent.vue'
import StoryList from './components/story-list.vue'
import BugList from './components/bug-list.vue'

export default {
  components: { FormComponent, StoryList, BugList},
  data() {
    return {
      formDisabled: false,
      storyDisabled: false,
      bugDisabled: false,
      showForm: false,
      showStoryList: false,
      showBugList: false,
    }
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm;
      this.storyDisabled = false;
      this.showStoryList = false;
      this.bugDisabled = false;
      this.showBugList = false;
    },
    toggleStoryList() {
      this.showStoryList = !this.showStoryList;
      this.formDisabled = false;
      this.bugDisabled = false;
      this.showForm = false;
      this.showBugList = false;
    },
    toggleBugList() {
      this.showBugList = !this.showBugList;
      this.formDisabled = false;
      this.storyDisabled = false;
      this.showForm = false;
      this.showStoryList = false
    },
  },
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

body {
  background-color: darkcyan;
}

h1 {
  text-align: center;
}

button {
  float: right;
  margin: 0px 10px 0px 20px;
  padding: 10px 20px 10px 20px;
  border: none;
  border-radius: 10px;
}

button:hover {
  background-color: cadetblue;
}
</style>




