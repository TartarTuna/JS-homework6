<template>
<div>
    <div class="container">
      <form class="form-signin" @submit.prevent="signin">
        <h1 class="h3 mb-3 font-weight-normal">請先登入</h1>

        <div class="form-group">
          <label for="inputEmail" class="sr-only">Email address</label>
          <input
            id="inputEmail"
            v-model="user.email"
            type="email"
            class="form-control"
            placeholder="Email address"
            required
            autofocus
          />
        </div>
        <div class="form-group">
          <label for="inputPassword" class="sr-only">Password</label>
          <input
            id="inputPassword"
            v-model="user.password"
            type="password"
            class="form-control"
            placeholder="Password"
            required
          />
        </div>
        <button class="btn btn-lg btn-primary btn-block" type="submit">登入</button>
        <br>
        <button class="btn btn-outline-primary btn-block" type="button"  @click="signout">
        登出
        </button>
        <p class="mt-5 mb-3 text-muted">&copy; 2020~∞ - 六角學院</p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      user: {
        email: '',
        passward: ''
      },
      token: ''
    }
  },
  methods: {
    signin () {
      const api = `${process.env.VUE_APP_APIPATH}auth/login`
      this.$http.post(api, this.user)
        .then((res) => {
          const token = res.data.token
          const expired = res.data.expired
          // 把 token 和 expire 寫入 cookie
          // 把 expire 轉換成固定格式
          document.cookie = `token=${token};expires=${new Date(
            expired * 1000)};`
          this.$router.push('admin/products')
        }).catch((err) => {
          console.log(err)
        })
    },
    signout () {
      document.cookie = 'hexToken=;expires=;'
      console.log('token 已清除')
    }
  }
}
</script>

<style lang="scss">
    html,body {
        height: 100vh;
        text-align: center;
    }
    body {
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>
