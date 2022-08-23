<template>
  <va-affix :offset-top="0">
    <va-navbar class="navbar" color="dark">
      <template #left>
        <va-navbar-item>
          <router-link to="/"
            ><img class="logo" src="@/assets/img/logo.png" alt="logo"
          /></router-link>
        </va-navbar-item>
      </template>
      <template #right>
        <!-- <va-navbar-item
          ><router-link class="item" to="/">Home</router-link></va-navbar-item
        > -->
        <va-navbar-item
          ><router-link class="item" to="/characters"
            >Characters</router-link
          ></va-navbar-item
        >
        <va-navbar-item
          ><router-link class="item" to="/places"
            >Places</router-link
          ></va-navbar-item
        >
        <va-navbar-item>
          <router-link class="item" to="/episodes">Episodes </router-link>
        </va-navbar-item>
      </template>
    </va-navbar>
  </va-affix>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.item {
  color: white;
  text-decoration: none;
  font-size: medium;
  padding: 10px 15px;
}
.item:focus {
  color: #00a7bd;
}
.item:hover {
  background-color: #363636;
  color: #00a7bd;
  border-radius: 3px;
}
.navbar {
  overflow: hidden;
}
.logo {
  width: 170px;
  height: auto;
}
</style>
