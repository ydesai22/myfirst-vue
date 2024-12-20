<template>
  <div class="second-page">
    <h1>Work Tracker</h1>
    <p>Track your work with Start, Confirm, and Finish buttons!</p>
    <button :disabled="!isStartEnabled" @click="openModal('start')">Start Work</button>
    <button :disabled="!isFinishEnabled" @click="openModal('finish')">Finish Work</button>

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
      isStartEnabled: true, // Start button is enabled initially
      isFinishEnabled: false, // Finish button is disabled initially
      showModal: false, // Controls modal visibility
      modalMessage: "", // Message displayed in the modal
      currentAction: "", // Tracks the current action (start/finish)
    };
  },
  methods: {
    // Open the modal with a specific action
    openModal(action) {
      this.currentAction = action;
      this.modalMessage =
        action === "start"
          ? "Are you sure you want to start work?"
          : "Are you sure you want to finish work?";
      this.showModal = true;

      // Store modal state in localStorage
      localStorage.setItem("showModal", true);
      localStorage.setItem("modalMessage", this.modalMessage);
      localStorage.setItem("currentAction", this.currentAction);
    },

    // Confirm the action and update button states
    confirmAction() {
      if (this.currentAction === "start") {
        this.isStartEnabled = false; // Disable Start button
        this.isFinishEnabled = true; // Enable Finish button
      } else if (this.currentAction === "finish") {
        this.isStartEnabled = true; // Enable Start button
        this.isFinishEnabled = false; // Disable Finish button
      }

      // Reset modal state and clear from localStorage
      this.closeModal();
      localStorage.removeItem("showModal");
      localStorage.removeItem("modalMessage");
      localStorage.removeItem("currentAction");
    },

    // Close the modal without changing states
    closeModal() {
      this.showModal = false;
      this.currentAction = "";

      // Clear modal data from localStorage
      localStorage.removeItem("showModal");
      localStorage.removeItem("modalMessage");
      localStorage.removeItem("currentAction");
    },

    // Restore state from localStorage on page load
    restoreState() {
      // Restore modal state
      this.showModal = JSON.parse(localStorage.getItem("showModal")) || false;
      this.modalMessage = localStorage.getItem("modalMessage") || "";
      this.currentAction = localStorage.getItem("currentAction") || "";

      // Restore button states
      this.isStartEnabled =
        JSON.parse(localStorage.getItem("isStartEnabled")) ?? true;
      this.isFinishEnabled =
        JSON.parse(localStorage.getItem("isFinishEnabled")) ?? false;
    },
  },
  mounted() {
    this.restoreState(); // Restore state when the component loads
  },
};
</script>

<style scoped>
/* Page Background */
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

/* Buttons */
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

/* Modal Overlay */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6); /* Dark semi-transparent background */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

/* Modal Box */
.modal {
  background: white; /* Bright background for contrast */
  color: #333; /* Dark text for readability */
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  max-width: 400px;
  width: 90%;
  animation: fadeIn 0.5s ease-in-out;
}

/* Modal Text */
.modal p {
  font-size: 1.2em;
  margin-bottom: 20px;
}

/* Modal Buttons */
.modal button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  transition: all 0.2s ease;
}

.modal button:first-of-type {
  background-color: #4caf50;
  color: white;
}

.modal button:first-of-type:hover {
  background-color: #45a049;
}

.modal button:last-of-type {
  background-color: #f44336;
  color: white;
}

.modal button:last-of-type:hover {
  background-color: #e53935;
}

/* Animations */
@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: scale(0.9);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
