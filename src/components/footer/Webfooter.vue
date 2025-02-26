<template>
  <div class="hero">
    <div class="container-foodnow">
      <img src="@/assets/img/logo-alt.svg" alt="" />
      <p>find Us :</p>
      <div class="left-logo">
        <div class="icon-wrapper fb-logo">
          <img src="@/assets/img/icons/facebook.svg" alt="" width="20px" />
        </div>
        <div class="icon-wrapper ig-logo">
          <img src="@/assets/img/icons/instagram.svg" alt="" width="35px" />
        </div>
        <div class="icon-wrapper yt-logo">
          <img src="@/assets/img/icons/youtube.svg" alt="" width="40px" />
        </div>
      </div>
    </div>
    <div class="container-navigation">
      <p class="navigation-title">Navigation</p>
      <div class="navigation-detail">
        <div>
          <p>Home</p>
          <p>Order</p>
          <p>About</p>
          <p>Blog</p>
        </div>
        <div>
          <p>Contact</p>
          <p>Login</p>
          <p>Register</p>
        </div>
      </div>
    </div>
    <div class="container-contact">
      <p class="contact-title">Contact</p>
      <div class="detail-contact">
        <img src="@/assets/img/icons/mail.svg" alt="" />
        <p>Food.now@gmail.com</p>
      </div>
      <div class="detail-contact">
        <img src="@/assets/img/icons/phone.svg" alt="" />
        <p>+62848477102943</p>
      </div>
      <div class="detail-contact">
        <img src="@/assets/img/icons/whatsapp.svg" alt="" />
        <p>+628184938494</p>
      </div>
    </div>
    <div class="container-location">
      <p class="location-title">Location</p>
      <div class="location-detail">
        <img src="@/assets/img/icons/location.svg" alt="" />
        <p>Kerobokan</p>
      </div>
      <p>
        Jl. Raya Kerobokan Br Taman, Kuta No.98,<br />
        Kerobokan Kelod, Kec. Kuta Utara,<br />
        Kabupaten Badung, Bali 80361
      </p>
    </div>
  </div>
  <div class="hr">
    <hr />
  </div>
  <div class="copyright">
    <p class="first-cp">
      Copyright © 2022 Foodnow. All Rights Reserved. Powered by PT. Timedoor
      Indonesia. | Privacy Policy
    </p>
    <p class="second-cp">
      This site is protected by reCAPTCHA and the Google Privacy Policy and
      Terms of Service apply.
    </p>
  </div>
</template>

<style scoped>
.hero {
  margin-top: 80px;
  padding: 0 100px;
  display: flex;
  justify-content: space-between;
  margin-bottom: -80px;
}

.container-foodnow p {
  color: #e77e23;
  font-size: 27px;
  margin-top: 50px;
  font-weight: 600;
}

.left-logo {
  display: flex;
  align-items: center;
  gap: 15px;
}

.icon-wrapper {
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  border: 2px solid #e77e23;
  overflow: hidden;
  background-color: white;
}

.icon-wrapper img {
  max-width: 70%;
  max-height: 70%;
}

.navigation-detail {
  display: flex;
  justify-content: space-between;
}

.detail-contact {
  display: flex;
}

.detail-contact img {
  margin-right: 10px;
}

.detail-contact p {
  font-size: 18px;
}

.location-detail {
  display: flex;
}

.navigation-title {
  color: #e77e23;
  font-size: 27px;
  margin-top: -20px;
  font-weight: 600;
}

.contact-title {
  color: #e77e23;
  font-size: 27px;
  margin-top: -20px;
  font-weight: 600;
}

.location-title {
  color: #e77e23;
  font-size: 27px;
  margin-top: -20px;
  font-weight: 600;
}

.navigation-detail p {
  font-size: 18px;
  color: #4d4d4d;
}

.container-location p {
  font-size: 18px;
}

.hr {
  padding: 0 100px;
  margin-top: 150px;
  color: #c4c4c4;
}

.copyright {
  margin-top: 20px;
  font-size: 14px;
  color: #555;
}

.first-cp {
  margin-left: 600px;
}

.second-cp {
  margin-left: 613px;
}
</style>
