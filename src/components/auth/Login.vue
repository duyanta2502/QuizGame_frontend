<template>
    <div>
        <section class="bg-light py-3 py-md-5">
            <div class="container">
                <div class="row justify-content-center">
                    <div class="col-12 col-sm-10 col-md-8 col-lg-6 col-xl-5 col-xxl-4">
                        <div class="card border border-light-subtle rounded-3 shadow-sm mt-5">
                            <div class="card-body p-3 p-md-4 p-xl-5">
                                <div class="text-center mb-3">
                                    <a href="#!">
                                        <img src="https://assets-cdn.kahoot.it/auth/assets/topbar_logo_purple-BNw_v6xK.svg"
                                            alt="Logo" width="250">
                                    </a>
                                </div>
                                <h2 class="fs-6 fw-normal text-center text-secondary mb-4">Sign in to your account</h2>
                                <form method="POST" action="/login">
                                    <!-- Alert for errors (dynamic rendering can be added via JS if needed) -->
                                    <div class="alert alert-danger d-none" id="error-message" role="alert"></div>

                                    <div class="row gy-2 overflow-hidden">
                                        <div class="col-12">
                                            <div class="form-floating mb-3">
                                                <input type="email" v-model="formData.email" class="form-control" name="email" id="email"
                                                    placeholder="name@example.com" required>
                                                <label for="email" class="form-label">Email Address</label>
                                            </div>
                                        </div>

                                        <div class="col-12">
                                            <div class="form-floating mb-3">
                                                <input type="password" v-model="formData.password" class="form-control" name="password"
                                                    id="password" placeholder="Password" required>
                                                <label for="password" class="form-label">Password</label>
                                            </div>
                                        </div>

                                        <div class="col-12">
                                            <div class="d-flex gap-2 justify-content-between">
                                                <div class="form-check">
                                                    <input class="form-check-input" type="checkbox" name="rememberMe"
                                                        id="rememberMe">
                                                    <label class="form-check-label text-secondary" for="rememberMe">
                                                        Keep me logged in
                                                    </label>
                                                </div>
                                                <a href="/forgot-password"
                                                    class="link-primary text-decoration-none">Forgot password?
                                                </a>
                                            </div>
                                        </div>

                                        <div class="col-12">
                                            <div class="d-grid my-3">
                                                <button class="btn btn-primary btn-lg" type="submit">Login</button>
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
                                            <p class="m-0 text-secondary text-center">Don't have an account? <a
                                                    href="/register" class="link-primary text-decoration-none">Signup
                                                </a>
                                            </p>
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
import axios from "axios";
import { reactive, ref } from "vue";

export default {
  name: "Login",
  setup() {
    const formData = reactive({
      email: "",
      password: "",
    });

    const errorMessage = ref("");

    const handleLogin = async () => {
      try {
        // Gửi request đăng nhập đến API
        const response = await axios.post("http://localhost:8000/api/login", formData, {
          headers: {
            Accept: "application/json",
          },
        });

        // Lưu token vào localStorage
        localStorage.setItem("auth_token", response.data.token);

        alert("Đăng nhập thành công!");
        console.log("User Info:", response.data.user);

        // Điều hướng sang trang chính hoặc dashboard
        window.location.href = "/";
      } catch (error) {
        if (error.response && error.response.status === 401) {
          errorMessage.value = "Email hoặc mật khẩu không chính xác!";
        } else {
          errorMessage.value = "Đã xảy ra lỗi. Vui lòng thử lại!";
        }
      }
    };

    return {
      formData,
      handleLogin,
      errorMessage,
    };
  },
};
</script>

<style scoped>
.msg-error {
    color: red
}
</style>