<template>
  <div class="second-page">
    <h1>Work Tracker</h1>
    <p>Track your work with Start and Stop buttons!</p>

    <!-- Task Input -->
    <div class="task-input">
      <label for="numTasks">No of Tasks (1-25): </label>
      <input
        type="number"
        id="numTasks"
        v-model.number="numTasks"
        min="1"
        max="25"
        placeholder="Enter number of tasks"
      />
      <button :disabled="!isTaskInputValid" @click="generateTasks">Generate Tasks</button>
    </div>

    <!-- Task Table -->
    <table v-if="tasks.length > 0" class="task-table">
      <thead>
        <tr>
          <th>Task Name</th>
          <th>Start</th>
          <th>Stop</th>
          <th>Start Count</th>
          <th>Stop Count</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td>
            <button
              :disabled="task.isStarted"
              @click="startTask(index)"
              class="btn-start"
            >
              Start
            </button>
          </td>
          <td>
            <button
              :disabled="!task.isStarted || task.isStopped"
              @click="stopTask(index)"
              class="btn-stop"
            >
              Stop
            </button>
          </td>
          <td>{{ task.startCount }}</td>
          <td>{{ task.stopCount }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numTasks: null, // Number of tasks input
      tasks: [], // Task details
    };
  },
  computed: {
    // Validate task input between 1 and 25
    isTaskInputValid() {
      return this.numTasks >= 1 && this.numTasks <= 25;
    },
  },
  methods: {
    // Generate tasks based on input
    generateTasks() {
      this.tasks = Array.from({ length: this.numTasks }, (_, index) => ({
        name: `Task ${index + 1}`,
        isStarted: false,
        isStopped: false,
        startCount: 0,
        stopCount: 0,
      }));
    },
    // Start a specific task
    startTask(index) {
      const task = this.tasks[index];
      task.isStarted = true;
      task.isStopped = false;
      task.startCount += 1;
    },
    // Stop a specific task
    stopTask(index) {
      const task = this.tasks[index];
      task.isStarted = false;
      task.isStopped = true;
      task.stopCount += 1;
    },
  },
};
</script>

<style scoped>
/* Page Styles */
.second-page {
  text-align: center;
  margin-top: 50px;
  background: linear-gradient(135deg, #62823c, #96cadc);
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
  font-family: 'Arial', sans-serif;
}

/* Task Input Section */
.task-input {
  margin-bottom: 20px;
}

input {
  padding: 8px;
  font-size: 1rem;
  margin-right: 10px;
}

button {
  margin: 15px;
  padding: 12px 30px;
  font-size: 18px;
  border-radius: 25px;
  cursor: pointer;
  border: none;
  transition: all 0.3s ease;
}

button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

button:not(:disabled) {
  background-color: #4caf50;
  color: white;
}

button:not(:disabled):hover {
  background-color: #45a049;
  transform: scale(1.05);
}

/* Task Table */
.task-table {
  margin-top: 20px;
  border-collapse: collapse;
  width: 80%;
}

.task-table th,
.task-table td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: center;
}

.task-table th {
  background-color: #4caf50;
  color: white;
}

.task-table td {
  background-color: #f4f4f4;
  color: #333;
}

.task-table td button {
  padding: 5px 15px;
  font-size: 16px;
  border-radius: 5px;
  transition: all 0.3s ease;
}

.task-table td button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

.task-table td button:not(:disabled):hover {
  background-color: #45a049;
  transform: scale(1.05);
}
</style>
