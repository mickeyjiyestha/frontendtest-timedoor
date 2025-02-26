<script setup></script>
<template>
  <header class="hero">
    <nav class="navbar">
      <div class="section-1">
        <img src="@/assets/img/logo.svg" alt="Logo" />
      </div>
      <div class="section-2">
        <p>Home</p>
        <p>Order</p>
        <p>About</p>
        <p>Blog</p>
        <p>Content Us</p>
      </div>
      <div class="section-3">
        <div>Login</div>
        <div class="btn-register">Register</div>
      </div>
    </nav>

    <div class="content-title">
      <p>Pizza Order</p>
    </div>
  </header>
</template>

<style scoped>
.hero {
  background-image: url("@/assets/img/hero.png");
  background-size: cover;
  background-position: center;
  min-height: 100vh;
}

.navbar {
  display: flex;
  color: white;
  align-items: center;
  justify-content: space-between;
  padding-top: 60px;
  font-weight: 500;
  font-size: 20px;
}

.section-1 {
  margin-left: 150px;
}

.section-1:hover {
  cursor: pointer;
}

.section-2 {
  display: flex;
}

.section-2 p {
  margin-left: 25px;
}

.section-2:hover {
  cursor: pointer;
}

.section-3 {
  display: flex;
  margin-right: 150px;
  align-items: center;
}

.section-3 div {
  margin-left: 60px;
}

.section-3:hover {
  cursor: pointer;
}

.btn-register {
  border-radius: 30px;
  background-color: orange;
  padding: 10px 25px;
}

.content-title {
  display: flex;
  color: orange;
  align-items: center;
  justify-content: center;
  margin-top: 250px;
  font-size: 80px;
}
</style>
