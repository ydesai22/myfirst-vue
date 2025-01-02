<template>
  <div class="second-page">
    <h1>Work Tracker</h1>
    <p>Track your work with Start, Confirm, and Finish buttons!</p>

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
        </tr>
      </tbody>
    </table>

    <!-- Modal -->
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <p>{{ modalMessage }}</p>
        <button @click="confirmAction">Yes</button>
        <button @click="closeModal">No</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numTasks: null, // Number of tasks input
      tasks: [], // Task details
      isStartEnabled: true, // Start button state
      isFinishEnabled: false, // Finish button state
      showModal: false, // Modal visibility
      modalMessage: "", // Modal message
      currentAction: "", // Current action in modal (start/finish)
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
      }));
    },
    // Start a specific task
    startTask(index) {
      this.tasks[index].isStarted = true;
    },
    // Stop a specific task
    stopTask(index) {
      this.tasks[index].isStopped = true;
    },
    // Open modal with specified action
    openModal(action) {
      this.currentAction = action;
      this.modalMessage =
        action === "start"
          ? "Are you sure you want to start work?"
          : "Are you sure you want to finish work?";
      this.showModal = true;

      // Save modal state in localStorage
      localStorage.setItem("showModal", true);
      localStorage.setItem("modalMessage", this.modalMessage);
      localStorage.setItem("currentAction", this.currentAction);
    },
    // Confirm action and update button states
    confirmAction() {
      if (this.currentAction === "start") {
        this.isStartEnabled = false;
        this.isFinishEnabled = true;
      } else if (this.currentAction === "finish") {
        this.isStartEnabled = true;
        this.isFinishEnabled = false;
      }
      this.closeModal();
      localStorage.removeItem("showModal");
      localStorage.removeItem("modalMessage");
      localStorage.removeItem("currentAction");
    },
    // Close the modal
    closeModal() {
      this.showModal = false;
      this.currentAction = "";
      localStorage.removeItem("showModal");
      localStorage.removeItem("modalMessage");
      localStorage.removeItem("currentAction");
    },
    // Restore state from localStorage
    restoreState() {
      this.showModal = JSON.parse(localStorage.getItem("showModal")) || false;
      this.modalMessage = localStorage.getItem("modalMessage") || "";
      this.currentAction = localStorage.getItem("currentAction") || "";
    },
  },
  mounted() {
    this.restoreState();
  },
};
</script>

<style scoped>
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
  background-color: #f4f4f4;
  color: #333;
}

/* Modal */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background: white;
  color: #333;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  max-width: 400px;
  width: 90%;
}

.modal button:first-of-type {
  background-color: #4caf50;
  color: white;
}

.modal button:last-of-type {
  background-color: #f44336;
  color: white;
}
</style>
