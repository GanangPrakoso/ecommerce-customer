<template>
  <div>
    <div class="loading" v-if="loading"></div>
    <div class="page" v-if="!loading">
      <div id="login">
        <div class="container h-100" style="padding-top: 130px;">
          <div class="d-flex justify-content-center h-100">
            <div class="user_card">
              <div class="d-flex justify-content-center">
                <div class="brand_logo_container">
                  <img
                    src="../assets/register.gif"
                    class="brand_logo"
                    alt="Logo"
                    @click="home"
                    style="cursor: pointer;"
                    
                  />
                </div>
              </div>
              <div class="d-flex justify-content-center form_container">
                <form id="login-form" @submit.prevent="register">
                   <div class="input-group mb-3">
                    <div class="input-group-append">
                      <span class="input-group-text">
                        <i class="fas fa-user"></i>
                      </span>
                    </div>
                    <input
                      type="text"
                      id="form-email-login"
                      class="form-control input_user"
                      placeholder="name"
                      v-model="name"
                    />
                  </div>
                  <div class="input-group mb-3">
                    <div class="input-group-append">
                      <span class="input-group-text">
                        <i class="fas fa-envelope"></i>
                      </span>
                    </div>
                    <input
                      type="text"
                      id="form-email-login"
                      class="form-control input_user"
                      placeholder="email"
                      v-model="email"
                    />
                  </div>
                  <div class="input-group mb-2">
                    <div class="input-group-append">
                      <span class="input-group-text">
                        <i class="fas fa-key"></i>
                      </span>
                    </div>
                    <input
                      type="password"
                      id="form-password-login"
                      class="form-control input_pass"
                      placeholder="password"
                      v-model="password"
                    />
                  </div>
                  <div class="d-flex justify-content-center login_container">
                    <button type="submit" name="button" class="btn login_btn mt-3">Register</button>
                  </div>
                </form>
              </div>
              <span class="mt-4" style="margin-left: auto; margin-right: auto">
                Back to
                <router-link class="register-link" to="/login">login</router-link>
              </span>
            </div>
          </div>
        </div>
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "../api/axiosInstance";
export default {
  name: `Login`,
  data() {
    return {
      name: '',
      email: "",
      password: "",
      loading: false
    };
  },
  methods: {
    home() {
       this.$router.push('/')
    },
    register() {
      this.loading = true;
      axios({
        method: `POST`,
        url: `/users/register`,
        data: {
          name: this.name,
          email: this.email,
          password: this.password
        }
      })
        .then(({ data }) => {
            Toastify({
              text: "Registered successfully, welcome to G&N",
              backgroundColor: "linear-gradient(to right, #DA22FF, #9733EE)",
              className: "info"
            }).showToast()
  
            setTimeout(() => {
              this.$router.push("/login")
            }, 1500)
          
        })
        .catch(err => {         
          this.loading = false;

          let error = err.response.data.errors
          Toastify({
            text: `${error}`,
            backgroundColor: "linear-gradient(to right, #DA22FF, #9733EE)",
            className: "info"
          }).showToast()
        });
    }
  }
};
</script>

<style scoped>
.loading {
  min-height: 100vh;
  background-image: url("../assets/loading.webp");
  height: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.page {
  background-image: url("../assets/6.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.login-container {
  margin-top: 5%;
  margin-bottom: 5%;
  background: transparent;
}
.login-form-1 {
  padding: 5%;
  box-shadow: 0 5px 8px 0 rgba(0, 0, 0, 0.2), 0 9px 26px 0 rgba(0, 0, 0, 0.19);
}
.login-form-1 h3 {
  text-align: center;
  color: #333;
}

.login-container form {
  padding: 10%;
}
.btnSubmit {
  width: 50%;
  border-radius: 1rem;
  padding: 1.5%;
  border: none;
  cursor: pointer;
}
.login-form-1 .btnSubmit {
  font-weight: 600;
  color: #fff;
  background-color: #0062cc;
}

.login-form-1 .ForgetPwd {
  color: #0062cc;
  font-weight: 600;
  text-decoration: none;
}

.nav-item {
  margin-top: 17px;
}

.user_card {
  height: 450px;
  width: 350px;
  margin-top: auto;
  margin-bottom: auto;
  background: #f1f0ee;
  position: relative;
  display: flex;
  justify-content: center;
  flex-direction: column;
  padding: 10px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  -webkit-box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2),
    0 6px 20px 0 rgba(0, 0, 0, 0.19);
  -moz-box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2),
    0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 5px;
  opacity: 0.95;
}
.brand_logo_container {
  position: absolute;
  height: 170px;
  width: 170px;
  top: -75px;
  border-radius: 50%;
  background: rgb(0, 0, 0);
  padding: 10px;
  text-align: center;
}
.brand_logo {
  height: 150px;
  width: 150px;
  border-radius: 50%;
  border: 2px solid white;
}
.form_container {
  margin-top: 100px;
}
.login_btn {
  width: 100%;
  background: #000000ce !important;
  color: white !important;
}
.login_btn:focus {
  box-shadow: none !important;
  outline: 0px !important;
}
.login_container {
  padding: 0 2rem;
}
.input-group-text {
  background: #000000ce !important;
  color: white !important;
  border: 0 !important;
  border-radius: 0.25rem 0 0 0.25rem !important;
}
.input_user,
.input_pass:focus {
  box-shadow: none !important;
  outline: 0px !important;
}
.custom-checkbox .custom-control-input:checked ~ .custom-control-label::before {
  background-color: #c0392b !important;
}
.register-link {
  color: #0062cc;
  cursor: pointer;
}
.register-link:hover {
  color: rgb(233, 32, 65);
}
</style>
