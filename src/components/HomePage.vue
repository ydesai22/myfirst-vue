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
  <!-- <template>
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
  </style> -->
  

  <template>
    <div class="home-page">
      <h1>Welcome to the Home Page</h1>
      <p>
        This is the starting point of our application. Click the button below to
        explore more...
      </p>
      <button class="btn" @click="goToSecondPage">Go to Second Page</button>
  
      <!-- Form Section -->
      <div class="form-container">
        <h2>Contact Us</h2>
        <p>We'd love to hear from you! Please fill out the form below:</p>
        <form @submit.prevent="handleSubmit">
          <!-- Name Input -->
          <div class="form-group">
            <label for="name">Name</label>
            <input
              type="text"
              id="name"
              v-model="formData.name"
              placeholder="Your Name"
              required
            />
          </div>
  
          <!-- Email Input -->
          <div class="form-group">
            <label for="email">Email</label>
            <input
              type="email"
              id="email"
              v-model="formData.email"
              placeholder="Your Email"
              required
            />
          </div>
  
          <!-- Phone Input -->
          <div class="form-group">
            <label for="phone">Phone</label>
            <input
              type="tel"
              id="phone"
              v-model="formData.phone"
              placeholder="Your Phone Number"
              pattern="[0-9]{10}"
              title="Enter a valid 10-digit phone number"
              required
            />
          </div>
  
          <!-- Submit Button -->
          <button class="btn" type="submit">Submit</button>
        </form>
      </div>
  
      <!-- Success Popup -->
      <div v-if="successPopup" class="popup success">
        <p>🎉 Form submitted successfully! Thank you for reaching out!</p>
        <button @click="closePopup">Close</button>
      </div>
  
      <!-- Error Popup -->
      <div v-if="errorPopup" class="popup error">
        <p>❌ Please fill in all fields correctly!</p>
        <button @click="closePopup">Close</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          name: "",
          email: "",
          phone: "",
        },
        successPopup: false,
        errorPopup: false,
      };
    },
    methods: {
      goToSecondPage() {
        this.$router.push("/second");
      },
      handleSubmit() {
        // Validate form
        if (
          this.formData.name &&
          this.formData.email &&
          this.formData.phone.length === 10
        ) {
          this.successPopup = true;
          console.log("Form submitted:", this.formData);
          this.resetForm();
        } else {
          this.errorPopup = true;
        }
      },
      resetForm() {
        this.formData = {
          name: "",
          email: "",
          phone: "",
        };
      },
      closePopup() {
        this.successPopup = false;
        this.errorPopup = false;
      },
    },
  };
  </script>
  
  <style scoped>
  /* Main Page Styling */
  .home-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: radial-gradient(circle, #87ceeb, #ffe4b5); /* 3D-like background */
    color: #333;
    text-align: center;
    font-family: "Poppins", sans-serif;
  }
  
  /* Header Styling */
  h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
    color: #2f4f4f;
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
  }
  
  p {
    font-size: 1.5rem;
    margin-bottom: 2rem;
    color: #2f4f4f;
  }
  
  /* Button Styling */
  .btn {
    padding: 10px 20px;
    font-size: 1.2rem;
    color: #fff;
    background: linear-gradient(45deg, #ff6347, #ff4500);
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: transform 0.3s ease, background-color 0.3s ease;
  }
  
  .btn:hover {
    background: linear-gradient(45deg, #ff4500, #ff6347);
    transform: scale(1.1);
  }
  
  /* Form Styling */
  .form-container {
    margin-top: 30px;
    padding: 20px;
    width: 80%;
    max-width: 500px;
    background: linear-gradient(145deg, #ffffff, #f0f0f0);
    border-radius: 12px;
    box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.2);
    text-align: left;
  }
  
  .form-container h2 {
    font-size: 2rem;
    margin-bottom: 10px;
    color: #444;
  }
  
  .form-container p {
    margin-bottom: 20px;
    font-size: 1rem;
    color: #666;
  }
  
  /* Form Fields */
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
    color: #444;
  }
  
  input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 1rem;
    transition: box-shadow 0.3s ease;
  }
  
  input:focus {
    border-color: #ff6347;
    box-shadow: 0 0 10px rgba(255, 99, 71, 0.5);
  }
  
  /* Popups */
  .popup {
    position: fixed;
    bottom: 20px;
    right: 20px;
    padding: 15px;
    border-radius: 8px;
    color: #fff;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    animation: fadeIn 0.5s ease-in-out;
  }
  
  .popup.success {
    background: #4caf50;
  }
  
  .popup.error {
    background: #f44336;
  }
  
  .popup button {
    margin-top: 10px;
    padding: 8px 12px;
    font-size: 1rem;
    border: none;
    border-radius: 5px;
    background: #fff;
    color: #444;
    cursor: pointer;
  }
  
  .popup button:hover {
    background: #f0f0f0;
  }
  
  /* Fade-in Animation */
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  </style>
  

  