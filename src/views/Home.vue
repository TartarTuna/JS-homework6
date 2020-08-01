<template>
  <div class="home">
    <div id="nav">
      <router-link to="/">Home</router-link>|
      <router-link to="/products">產品列表</router-link>|
      <router-link to="/cart">購物車</router-link>|
      <router-link to="/about">關於我們</router-link>|
      <router-link to="/payment">結帳</router-link>|
      <router-link to="/complete">結帳完成</router-link>|
      <router-link to="/admin">前往後臺</router-link>
    </div>
    <router-view></router-view>
  </div>
</template>
