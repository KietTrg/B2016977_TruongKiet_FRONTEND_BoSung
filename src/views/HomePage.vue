<template>
  <div class="home">
    <div class="content">
      <h1>CHÀO MỪNG BẠN ĐẾN VỚI ỨNG DỤNG QUẢN LÝ DANH BẠ</h1>
      <div v-if="name == ''" class="abc">
        <h2>Tạo Tài Khoản</h2>
        <RouterLink class=" link" to="/signup">Signup</RouterLink>
        <h2>Đăng Nhập</h2>
        <RouterLink class="link" to="/login">Login</RouterLink>
      </div>
      <div class="d-flex justify-content-between align-items-center" v-if="name != ''">
        <div>
          <div>
            <h4>Xin chào: {{ name }}</h4>
            <h4>Tài khoản của bạn: {{ email }}</h4>
          </div>
          <button @click="logout">Logout</button>
        </div>
        <router-link :to="{ name: 'contactbook' }" class="nav-link link">
          <i class="fas fa-address-book"></i>
          Đi đến danh bạ
          <i class="fa-solid fa-caret-right"></i>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      name: "",
      email: ""
    };
  },

  mounted() {
    axios.get("http://localhost:3000/user", { headers: { token: localStorage.getItem("token") } })
      .then(res => {
        this.name = res.data.user.name;
        this.email = res.data.user.email;
      });
  },

  methods: {
    logout() {
      localStorage.clear();
      this.$router.go("/");
    }
  }
};
</script>

<style scoped>
template{
  position: relative;

}
.content{
  position: absolute;
  top: 50%;
  /* left: 50%; */
  /* transform: translateX(-50%); */
  transform: translateY(-50%);
}


button {
  width: 200px;
  height: 50px;
  padding: 5px 15px;
  font-size: 25px;
  border: 1px solid #333;
  border-radius: 50px;
  color: #333;
  background-color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #333;
  color: #fff;

}

button:focus {
  outline: none;
}
h2{
  margin-bottom: 20px;
}
.link {
  padding: 5px 15px;
  font-size: 25px;
  border: 1px solid #333;
  border-radius: 50px;
  color: #333;
  text-decoration: none;
}

.link:hover {
  background-color: #333;
  color: #fff;

}
</style>