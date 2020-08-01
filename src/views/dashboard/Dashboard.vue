<template>
  <div class="dashboard">
    <div id="nav">
      <router-link to="/admin">後臺首頁</router-link>|
      <router-link to="/admin/products">後台產品列表</router-link>|
      <router-link to="/admin/coupons">優惠券</router-link>|
      <router-link to="/admin/orders">訂單列表</router-link>|
      <router-link to="/admin/images">圖片儲存列表</router-link>|
      <router-link to="/">回到前臺</router-link>
    </div>
    <router-view v-if="checkSuccess" :token="token"></router-view>
  </div>
</template>

<script>
export default {
  data () {
    return {
      token: '',
      checkSuccess: false
    }
  },
  created () {
    this.checkLogin()
  },
  methods: {
    checkLogin () {
      this.token = document.cookie.replace(/(?:(?:^|.*;\s*)token\s*=\s*([^;]*).*$)|^.*$/, '$1')
      this.$http.defaults.headers.common.Authorization = `Bearer ${this.token}`

      const api = `${process.env.VUE_APP_APIPATH}auth/check`
      this.$http.post(api, {
        api_token: this.token
      })
        .then(res => {
          console.log(res)
          this.checkSuccess = true
        })
        .catch(err => {
          console.log(err)
          this.$router.push('/login')
        })
    }
  }
}
</script>
