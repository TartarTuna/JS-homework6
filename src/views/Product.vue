<template>
  <div class>
    <h2>單一產品頁</h2>
    <h3>{{ product.title }}</h3>
    <p>{{ product.description }}</p>
  </div>
</template>

<script>
export default {
  data () {
    return {
      product: {}
    }
  },
  created () {
    const { id } = this.$route.params

    const url = `${process.env.VUE_APP_APIPATH}${process.env.VUE_APP_UUID}/ec/product/${id}`
    this.$http.get(url).then(res => {
      console.log(res)
      this.product = res.data.data
    })
  }
}
</script>
