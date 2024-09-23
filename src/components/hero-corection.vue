<script>
export default {
  data() {
    return {
      tasks: [], // Initially an empty array for tasks
      newTask: '',
      removeLogo: '<i class="fa-solid fa-x"></i>',
    };
  },
  methods: {
    addTask() {
      if (this.newTask === '') {
        alert('This field cannot be empty');
      } else {
        // Add the new task to the tasks array
        this.tasks.push({ title: this.newTask, checked: false });
        // Clear the input field
        this.newTask = '';
      }
    },
    toggleCheck(task) {
      // Toggle the checked status of the task
      task.checked = !task.checked;
    },
    removeTask(index) {
      // Remove the task from the tasks array
      this.tasks.splice(index, 1);
    },
    addEventListener() {
      const listContainer = this.$refs.listContainer;

      // Arrow function to retain `this` context
      listContainer.addEventListener('click', (mouseclick) => {
        if (mouseclick.target.tagName === 'LI') {
          mouseclick.target.classList.toggle('checked');
        } else if (mouseclick.target.tagName === 'I') {
          mouseclick.target.closest('li').remove();
        }
      });
    },
  },
  mounted() {
    this.addEventListener(); // Call addEventListener properly
  },
};
</script>

<template>
  <div class="container">
    <div class="to-do">
      <h2>To-Do List</h2>
      <div class="row">
        <input
          type="text"
          id="input-box"
          placeholder="Add your task"
          v-model="newTask"
        />
        <button @click="addTask">Add Task</button>
      </div>

      <ul id="list-container" ref="listContainer">
        <!-- Iterate over tasks, bind class and remove task on icon click -->
        <li
          v-for="(task, index) in tasks"
          :key="index"
          :class="{ checked: task.checked }"
          @click="toggleCheck(task)"
        >
          {{ task.title }}
          <span @click.stop="removeTask(index)">
            <i class="fa-solid fa-x"></i>
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  font-family: 'Poppins';
  box-sizing: border-box;
}

.container {
  width: 100%;
  height: 100vh;
  background: linear-gradient(140deg, #153677, #4e085f);
  padding: 10px;
}

.to-do {
  width: 100%;
  max-width: 540px;
  background: #ffff;
  margin: 100px auto 20px;
  padding: 30px;
  border-radius: 30px;
}

.to-do h2 {
  color: #002765;
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #edeef0;
  border-radius: 30px;
  padding-left: 20px;
  margin-bottom: 25px;
}

input {
  flex: 1;
  border: 0;
  outline: none;
  background: transparent;
  padding: 10px;
}

button {
  border: none;
  outline: none;
  padding: 16px 50px;
  background: #ff5945;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  border-radius: 40px;
}

ul li {
  list-style: none;
  font-size: 17px;
  padding: 12px 8px 12px 50px;
  cursor: pointer;
  user-select: none;
  position: relative;
}

ul li::before {
  content: '';
  position: absolute;
  height: 28px;
  width: 28px;
  border-radius: 50%;
  background-image: url(/src/assets/images/unchecked.png);
  background-size: cover;
  background-position: center;
  top: 12px;
  left: 8px;
}

ul li.checked {
  color: #555;
  text-decoration: line-through;
}

ul li.checked::before {
  background-image: url(/src/assets/images/checked.png);
}

ul li span {
  right: 0;
  font-size: 16px;
  position: absolute;
}

ul li span:hover {
  transition: ease-in 0.2s;
  color: #1f90b3;
}
</style>
