<!-- <template>
    <div>
      <h1>Second Page</h1>
      <button @click="goBack">Go Back</button>
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
  </script> -->
  <template>
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
  
  