<template>
  <div class>
    <h2>後臺產品列表</h2>
    <table>
      <tr v-for="item in products" :key="item.id">
        <td>{{ item.title }}</td>
        <td>{{ item.price }}</td>
        <td>{{ item.content }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      products: []
    }
  },
  props: ['token'],
  created () {
    const url = `${process.env.VUE_APP_APIPATH}${process.env.VUE_APP_UUID}/ec/products`
    this.$http.get(url).then(res => {
      console.log(res)
      this.products = res.data.data
    })
  }
}
</script>
