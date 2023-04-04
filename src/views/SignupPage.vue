<template>
    <div class="signup">
        <h2>Đăng Kí</h2>
        <div class="Name">
            <label>Tên Tài Khoản:</label> 
            <input type="text" v-model="name">
        </div ><br>
        <div class="email">
            <label>Tên Đăng Nhập:</label> 
            <input type="text" v-model="email">
        </div ><br>
        <div class="pass">
            <label>Password:</label> 
            <input type="password" v-model="password">
        </div><br>
        <button @click="signup">Signup</button>
        <p>{{ error }}</p>
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "comp-signup",
    data() {
        return {
            name: "",
            email: "",
            password: "",
            error: ""
        };
    },
    methods: {
        signup() {
            let newUser = {
                name: this.name,
                email: this.email,
                password: this.password
            };
            axios.post("http://localhost:3000/signup", newUser)
                .then(() => {
                    this.error = "",
                        this.$router.push("/login");
                })
                .catch(() => {
                    this.error = "Tên đăng nhập đã được sử dụng";
                });

        }
    }
};
</script>

<style scoped>
template {
  position: relative;
}
.signup {
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
.signup input {
  margin-bottom: 5px;
  border-radius: 5px;
  margin-left: 5px;
}
.Name, .email, .pass{
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