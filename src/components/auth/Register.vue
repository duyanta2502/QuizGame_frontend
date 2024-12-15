<template>
    <div>
        <section class="bg-light py-3 py-md-5">
            <div class="container">
                <div class="row justify-content-center">
                    <div class="col-12 col-sm-10 col-md-8 col-lg-6 col-xl-5 col-xxl-4">
                        <div class="card border border-light-subtle rounded-3 shadow-sm">
                            <div class="card-body p-3 p-md-4 p-xl-5">
                                <div class="text-center mb-3">
                                    <a href="#!">
                                        <img src="https://assets-cdn.kahoot.it/auth/assets/topbar_logo_purple-BNw_v6xK.svg"
                                            alt="BootstrapBrain Logo" width="250">
                                    </a>
                                </div>
                                <h2 class="fs-6 fw-normal text-center text-secondary mb-4">Sign up to your account</h2>
                                <form @submit.prevent="handleSubmit" method="POST" action="/register">
                                    <div class="row gy-2 overflow-hidden">
                                        <div class="col-12">
                                            <div class="form-floating mb-3">
                                                <input type="text" v-model="formData.name" class="form-control"
                                                    name="name" id="name" placeholder="Your Name" required>
                                                <label for="name" class="form-label">Name</label>
                                            </div>
                                        </div>
                                        <div class="col-12">
                                            <div class="form-floating mb-3">
                                                <input type="email" v-model="formData.email" class="form-control"
                                                    name="email" id="email" placeholder="name@example.com" required>
                                                <label for="email" class="form-label">Email Address</label>
                                            </div>
                                        </div>
                                        <div class="col-12">
                                            <div class="form-floating mb-3">
                                                <input type="password" v-model="formData.password" class="form-control"
                                                    name="password" id="password" placeholder="Password" required>
                                                <label for="password" class="form-label">Password</label>
                                            </div>
                                        </div>
                                        <div class="col-12">
                                            <div class="form-floating mb-3">
                                                <input type="password" v-model="formData.password_confirmation"
                                                    class="form-control" name="password_confirmation"
                                                    id="password_confirmation" placeholder="Confirm Password" required>
                                                <label for="password_confirmation" class="form-label">Confirm
                                                    Password</label>
                                            </div>
                                        </div>
                                        <div class="col-12">
                                            <div class="d-grid my-3">
                                                <button class="btn btn-primary btn-lg" type="submit">Register</button>
                                            </div>
                                        </div>

                                        <div class="col-12">
                                            <div class="d-grid my-3">
                                                <button class="btn btn-light btn-lg border" type="button"
                                                    id="google-login">
                                                    <img src="https://assets-cdn.kahoot.it/auth/assets/google-D1qVgiZr.svg"
                                                        alt="Google Logo" width="20" class="me-2">
                                                    Continue with Google
                                                </button>
                                            </div>
                                        </div>

                                        <div class="col-12">
                                            <div class="d-grid my-3">
                                                <button class="btn btn-light btn-lg border" type="button"
                                                    id="github-login">
                                                    <img src="https://github.githubassets.com/assets/GitHub-Mark-ea2971cee799.png"
                                                        alt="Github Logo" width="20" class="me-2">
                                                    Continue with Github
                                                </button>
                                            </div>
                                        </div>

                                        <div class="col-12">
                                            <p class="m-0 text-secondary text-center">Have an account? <a href="/login"
                                                    class="link-primary text-decoration-none">Sign in</a></p>
                                        </div>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>

import axios from 'axios';
import { reactive } from 'vue';
export default {
  setup() {
    // Dữ liệu form
    const formData = reactive({
      name: '',
      email: '',
      password: '',
      password_confirmation: '',
    });

    // Hàm xử lý submit
    const handleSubmit = async () => {
      try {
        // Gửi request POST đến backend
        const response = await axios.post('http://localhost:8000/api/register', formData, {
          headers: {
            'Accept': 'application/json',
          },
        });
        console.log('Registration Success:', response.data);
        alert('Đăng ký thành công!');
      } catch (error) {
        console.error('Registration Failed:', error.response.data);
        alert('Lỗi: ' + JSON.stringify(error.response.data.errors));
      }
    };

    return {
      formData,
      handleSubmit,
    };
  },
};
</script>

<style scoped>
@import './src/assets/CSS/auth.css';

.msg-error {
    color: red
}
</style>