<template>
  <div class="container table">
      <table>
        <tr>
          <th>Product</th>
          <td v-for="product in productList" :item="product.selectedProduct" :key="product.index">{{ product.selectedProduct }}</td>
        </tr>
        <tr>
          <th>Bottle Size</th>
          <td></td>
        </tr>
        <tr>
          <th>Dilution Ratio</th>
          <td v-for="product in productList"
          :item="product.selectedRatio"
          :key="product.index">{{ product.selectedRatio }}</td>
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
          <td v-for="product in productList"
          :item="product.selectedPrice"
          :key="product.index">{{ "$" + product.selectedPrice }}</td>
        </tr>
        <tr>
          <th>$/EUG</th>
        </tr>
        <tr>
          <th>$/EUQ</th>
        </tr>
      </table>
      <button @click="clearTable">Clear Table</button>
    </div>
</template>

<script>
export default{
  name:'product-table',
  props: {
    product: {}
  },
  data(){
    return{
      productList: [],
    }
  },
  methods:{
    clearTable() {
      this.productList = [];
    }
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
