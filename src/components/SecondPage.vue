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

   <template>
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
  
        // Save states to localStorage
        localStorage.setItem("isStartEnabled", this.isStartEnabled);
        localStorage.setItem("isFinishEnabled", this.isFinishEnabled);
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
      this.restoreState(); // Restore states when page loads
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
  