<template>
  <div class="login">
    <h2>Đăng Nhập</h2>
    <div class="email">
      <label>Tên Đăng Nhập:</label>
      <input type="text" v-model="email">
    </div>
    <br>
    <div class="pass">
      <label>Password:</label>
      <input type="password" v-model="password">
    </div>
    <br>
    <button @click="login">Login</button>
    <p>{{ error }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "comp-signup",
  data() {
    return {
      email: "",
      password: "",
      error: ""
    };
  },
  methods: {
    login() {
      let user = {
        email: this.email,
        password: this.password
      };
      axios.post("http://localhost:3000/login", user)
        .then(res => {
          if (res.status === 200) {
            localStorage.setItem("token", res.data.token);
            this.$router.push("/");
          }
        })
        .catch(() => {
          this.error = "Tên đăng nhập hoặc password không hợp lệ";
        });
    }
  }
};
</script>

<style scoped>
template {
  position: relative;
}
.login {
  /* text-align: center; */
  position: absolute;
  top: 50%;
  left: 35%;
  transform: translateX(-35%);
  transform: translateY(-50%);
  /* background-color: #008cc8; */
  padding: 30px 20px 20px;
  border-radius: 10px;
  border: 1px solid #333;
}
h2{
  text-align: center;
  margin-bottom: 30px;
}
.login input {
  margin-bottom: 5px;
  border-radius: 5px;
  margin-left: 5px;
}
.email, .pass{
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: #333;

}
button{
  width: 50%;
  margin-left: 25%;
  margin-right: 25%;
  border-radius: 20px;
  background-color: white;
}
button:hover{
  background-color: #333;
  color: #fff;
}
p{
  color: #333;
}

</style>