<template>
  <section class="overflow-hidden min-h-[100vh] ">
    <img
      class="absolute inset-0 z-[-1] w-full h-[100vh] object-cover overflow-hidden"
      src="https://cdn.wallpapersafari.com/96/2/YyiJR7.jpg"
      alt=""
    />
    <section class=" flex justify-center items-center min-h-screen w-full">
      <div class="cont4page z-10 p-10">
        <h1
          class="text-[5rem] fredoka bg-gradient-to-r from-[#0766AD] via-[#190482] to-[#1640D6] bg-clip-text text-transparent"
        >
          Registration
        </h1>
        <input
          type="text"
          class="focus:text-white fredoka focus:bg-[#061c2a] focus:placeholder-gray-500 outline-none focus:ring focus:ring-[#1F51FF]"
          v-model="userName"
          placeholder="name"
        />
        <input
          class="focus:text-white fredoka focus:bg-[#061c2a] focus:placeholder-gray-500 outline-none focus:ring focus:ring-[#1F51FF]"
          :type="isPasswordVisible ? 'text' : 'password'"
          v-model="userPass"
          placeholder="password"
          id="passWord"
        />
        <input
          class="focus:text-white fredoka focus:bg-[#061c2a] focus:placeholder-gray-500 outline-none focus:ring focus:ring-[#1F51FF]"
          type="email"
          v-model="userEmail"
          placeholder="email"
        />
        <div class="cont4btn">
          <button @click="sendData">send</button>
          <button @click="togglePasswordVisibility" id="btn2">
            {{ isPasswordVisible ? "hide" : "show" }}
          </button>
        </div>
      </div>
    </section>
  </section>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      userName: "",
      userPass: "",
      userEmail: "",
      isPasswordVisible: false,
    };
  },
  methods: {
    validateForm() {
      if (this.userName.length < 2) {
        alert("Name must be at least 2 characters long.");
        return false;
      }
      if (!/[A-Za-z]/.test(this.userName)) {
        alert("Name must contain only letters.");
        return false;
      }
      if (/@/.test(this.userName)) {
        alert("Name must contain only letters.");
        return false;
      }

      if (this.userPass.length < 8) {
        alert("Password must be at least 8 characters long.");
        return false;
      }

      if (this.userEmail.length < 2) {
        alert("Email must be at least 2 characters long.");
        return false;
      }
      var validEmail =
        /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;
      if (!validEmail.test(this.userEmail)) {
        alert("Please enter a valid email address.");
        return false;
      }

      return true;
    },

    sendData() {
      if (!this.validateForm()) {
        return;
      }

      const userData = {
        name: this.userName,
        pass: this.userPass,
        email: this.userEmail,
      };

      fetch("https://reqres.in/api/users", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(userData),
      })
        .then((response) => response.json())
        .then((data) => {
          this.users.push(data);
          console.log(data);
        })
        .catch((error) => console.error("Error:", error));
    },

    togglePasswordVisibility() {
      this.isPasswordVisible = !this.isPasswordVisible;
    },
  },
};
</script>

<style scoped>
@tailwind base;
@tailwind components;
@tailwind utilities;


html,
section {
  margin: 0;
  padding: 0;
  height:100vh;
  overflow: hidden;
}

.fredoka {
  font-family: 'Fredoka', sans-serif;
}

.cont4page {
  background-color: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  width: 80%;
  max-width: 450px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 20px;
  border-radius: 30px;
  border: 1px solid white;
  box-shadow: 1px 24px 61px 10px rgba(230, 180, 105, 0.83);
  max-height: 80vh; /* Restrict height to avoid overflowing */
  height: auto;
}

.cont4btn {
  display: flex;
  gap: 30px;
}

input {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  border-radius: 10px;
  padding: 20px;
}

button {
  font-size: 20px;
  font-weight: 600;
  font-family: 'Fredoka', sans-serif;
  border-radius: 10px;
  padding: 15px 45px;
  background-color: rgb(38, 121, 193);
  color: rgb(27, 66, 142);
}

button:hover {
  background-color: rgb(27, 66, 142);
  color: white;
  transition: ease-in-out 300ms;
}

img {
  object-fit: cover;
}
</style>
