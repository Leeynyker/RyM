<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <va-carousel
      :items="items"
      stateful
      autoscroll
      :autoscrollInterval="5000"
      :indicators="false"
      :height="'70vh'"
      infinite
    >
      <!-- <template #default="{ index }">
        {{ index + 1 }}
      </template> -->
    </va-carousel>
    <div class="footer-home">
      <p class="footer-home__text">
        This project was carried out during the web development course with
        vue.js, for the ACM.UD group which was dictated by me
      </p>
      <div class="footer-home__img">
        <img class="logo-footer" src="@/assets/img/acm.svg" alt="logo acm"/>
        <img class="logo-footer" src="@/assets/img/logovue.png" alt="logo vue"/>
        <img class="logo-footer" src="@/assets/img/rym.png" alt="logo vue"/>
      </div>
      <div class="footer-footer">
        Leeynyker Andrés Montaño Ruiz
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
  },
  data() {
    return {
      value: 0,
      items: [
        require(`@/assets/img/c1.webp`),
        require(`@/assets/img/c2.webp`),
        require(`@/assets/img/c3.webp`),
        require(`@/assets/img/c4.webp`),
        require(`@/assets/img/c5.webp`),
        require(`@/assets/img/c6.webp`),
      ],
    };
  },
};
</script>
<style scoped>
.home{
  height: 100vh;
  width: 100%;
  background-color: rgb(40, 40, 40);  
}
.va-carousel__slide {
  font-size: 48px;
}
.footer-home {
  width: 100%;
  min-height: 20vh;
  overflow-x: hidden;
  background-color: rgb(40, 40, 40);
}
.footer-home__text{
  color: #f4f4f4;
  font-size: 1.8rem;
  font-weight: 100;
  font-family: "Lato", sans-serif;
  width: 40%;
  margin: 40px auto 30px auto;
}
.footer-home__img{
  display: flex;
  justify-content: center;
}
.logo-footer{
  width: 40px;
  height: auto;
  margin: 0 10px;
}
.footer-footer{
  color: #f4f4f4;
  font-size: 1rem;
  font-weight: 100;
  /* font-family: "Lato", sans-serif; */
  /* width: 40%; */
  margin: 20px auto 10px auto;
  letter-spacing: 1px;
}
</style>