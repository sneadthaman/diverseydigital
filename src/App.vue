<template>
  <div id="app">
    <header>
      <a href="http://www.diverseydigital.com/natools/"><img src="../assets/images/janvey_logo-125.png" alt="Diversey Logo" id="logo"></a>
      <h1>Dilution Control Calculator</h1>
    </header>

    <pick-products></pick-products>
    <product-table></product-table>

  </div>
</template>

<script>

import PickProduct from '@/components/PickProduct.vue';
import ProductTable from '@/components/ProductTable.vue';

export default {
  name: 'App',
  components: {
    'pick-products': PickProduct,
    'product-table': ProductTable,
  },
  data() {
    return {
    }
  },
}
</script>

<style>
@import '../assets/css/style.css';
</style>
