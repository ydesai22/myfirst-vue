<!-- <template>
    <div class="second-page">
      <h1>Welcome to the Second Page</h1>
      <p>You've made it here! Click below to go back to where you started.</p>
      <button class="btn" @click="goBack">Go Back</button>
    </div>
</template>
  
  <script>
  export default {
    methods: {
      goBack() {
        this.$router.push('/');
      },
    },
  };
  </script>
  
  <style scoped>
  .second-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: linear-gradient(135deg, #ffa07a, #afeeee);
    color: #333;
    text-align: center;
    font-family: 'Arial', sans-serif;
  }
  
  h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
    color: #2f4f4f;
  }
  
  p {
    font-size: 1.5rem;
    margin-bottom: 2rem;
    color: #2f4f4f;
  }
  
  .btn {
    padding: 10px 20px;
    font-size: 1.2rem;
    color: #fff;
    background-color: #4682b4;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .btn:hover {
    background-color: #5f9ea0;
  }
  </style>
  
   -->

   <!-- <template>
    <div class="second-page">
      <h1>Work Tracker</h1>
      <p>Track your work with start and finish buttons!</p>
  
      <button :disabled="!isStartEnabled" @click="handleClick('start')">Start Work</button>
      <button :disabled="!isFinishEnabled" @click="handleClick('finish')">Finish Work</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isStartEnabled: true,
        isFinishEnabled: false,
      };
    },
    methods: {
      handleClick(action) {
        if (action === "start") {
          this.isStartEnabled = false;
          this.isFinishEnabled = true;
          alert("Start Work clicked!");
        } else if (action === "finish") {
          this.isStartEnabled = true;
          this.isFinishEnabled = false;
          alert("Finish Work clicked!");
        }
  
        
        localStorage.setItem("isStartEnabled", this.isStartEnabled);
        localStorage.setItem("isFinishEnabled", this.isFinishEnabled);
      },
      restoreState() {

        this.isStartEnabled =
          JSON.parse(localStorage.getItem("isStartEnabled")) ?? true;
        this.isFinishEnabled =
          JSON.parse(localStorage.getItem("isFinishEnabled")) ?? false;
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
  }
  
  button {
    margin: 10px;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
  
  button:not(:disabled) {
    background-color: #4caf50;
    color: white;
  }
  
  button:last-of-type:not(:disabled) {
    background-color: #f44336;
  }
  </style>
   -->


   <template>
    <div class="second-page">
      <h1>Work Tracker</h1>
      <p>Track your work with Start, Confirm, and Finish buttons!</p>
  
      <!-- Buttons -->
      <button :disabled="!isStartEnabled" @click="showConfirm">Start Work</button>
      <button :disabled="!isFinishEnabled" @click="handleClick('finish')">Finish Work</button>
  
      <!-- Confirm Button Modal -->
      <div v-if="showConfirmModal" class="overlay">
        <div class="modal">
          <p>Are you sure you want to start work?</p>
          <button @click="confirmStart">Yes</button>
          <button @click="cancelConfirm">No</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isStartEnabled: true,
        isFinishEnabled: false,
        showConfirmModal: false, // Modal visibility state
      };
    },
    methods: {
      showConfirm() {
        this.showConfirmModal = true; // Show confirmation modal
      },
      confirmStart() {
        // Enable Finish button and disable Start button
        this.isStartEnabled = false;
        this.isFinishEnabled = true;
        this.showConfirmModal = false; // Hide modal
        alert("Start Work confirmed!");
  
        // Save states to localStorage
        localStorage.setItem("isStartEnabled", this.isStartEnabled);
        localStorage.setItem("isFinishEnabled", this.isFinishEnabled);
      },
      cancelConfirm() {
        this.showConfirmModal = false; // Close the modal without changing state
        alert("Start Work canceled!");
      },
      handleClick(action) {
        if (action === "finish") {
          // Enable Start button and disable Finish button
          this.isStartEnabled = true;
          this.isFinishEnabled = false;
          alert("Finish Work clicked!");
  
          // Save states to localStorage
          localStorage.setItem("isStartEnabled", this.isStartEnabled);
          localStorage.setItem("isFinishEnabled", this.isFinishEnabled);
        }
      },
      restoreState() {
        // Restore states from localStorage
        this.isStartEnabled =
          JSON.parse(localStorage.getItem("isStartEnabled")) ?? true;
        this.isFinishEnabled =
          JSON.parse(localStorage.getItem("isFinishEnabled")) ?? false;
      },
    },
    mounted() {
      this.restoreState(); // Restore states on page load
    },
  };
  </script>
  
  <style scoped>
  .second-page {
    text-align: center;
    margin-top: 50px;
    font-family: Arial, sans-serif;
  }
  
  button {
    margin: 10px;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
  
  button:not(:disabled) {
    background-color: #4caf50;
    color: white;
  }
  
  button:last-of-type:not(:disabled) {
    background-color: #f44336;
  }
  
  p {
    font-size: 18px;
    margin-top: 20px;
    color: #555;
  }
  
  /* Overlay Styles */
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
  
  /* Modal Styles */
  .modal {
    background: white;
    padding: 20px;
    border-radius: 8px;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  
  .modal button {
    margin: 10px;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
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
  