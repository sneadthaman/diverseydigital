<template>
  <div class="container table">
      <table>
        <tr>
          <th>Product</th>
          <td v-for="product in productList" :item="product.selectedProduct" :key="product.index">{{ product.selectedProduct }}</td>
        </tr>
        <tr>
          <th>Bottle Size</th>
        </tr>
        <tr>
          <th>Dilution Ratio</th>
        </tr>
        <tr>
          <th>Bottles/Case</th>
        </tr>
        <tr>
          <th>EUG/Bottle</th>
        </tr>
        <tr>
          <th>EUG/Case</th>
        </tr>
        <tr>
          <th>EUQ/Bottle</th>
        </tr>
        <tr>
          <th>EUQ/Case</th>
        </tr>
        <tr>
          <th>$/Case</th>
        </tr>
        <tr>
          <th>$/EUG</th>
        </tr>
        <tr>
          <th>$/EUQ</th>
        </tr>
      </table>
    </div>
</template>

<script>
export default{
  name:'product-table',
  props: {
    product: {
      brand: '',
      selectedProduct: '',
      category: '',
      ratio: '',
      price: '',
    }
  },
  data(){
    return{
      productList: [],
    }
  },
  methods:{
  },
  watch: {
    product: function() {
      this.productList.push(this.product);
      console.log(this.productList);
    }
  }
}
</script>

<style scoped>
</style>
