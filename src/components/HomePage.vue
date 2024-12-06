<!-- <template>
    <div>
      <h1>Home Page</h1>
      <button @click="goToSecondPage">Go to Second Page</button>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      goToSecondPage() {
        this.$router.push('/second');
      },
    },
  };
  </script> -->
  <template>
    <div class="home-page">
      <h1>Welcome to the Home Page</h1>
      <p>This is the starting point of our application. Click the button below to explore more...</p>
      <button class="btn" @click="goToSecondPage">Go to Second Page</button>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      goToSecondPage() {
        this.$router.push('/second');
      },
    },
  };
  </script>
  
  <style scoped>
  .home-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: linear-gradient(135deg, #89cff0, #f0e68c);
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
    background-color: #ff6347;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .btn:hover {
    background-color: #ff4500;
  }
  </style>
  