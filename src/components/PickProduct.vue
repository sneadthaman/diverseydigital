<template>
<div>
  <h2>Fill out the form to add a row to the table below</h2>
    <div class="container">
      <label for="platform">Dilution Control Platform</label>
      <select id="platform" name="platform" v-model="selectedBrand">
        <option value="" disabled>--Select a Platform--</option>
        <optgroup label="Diversey">
          <option v-for="brand in brands" :key="brand.id">{{ brand }}</option>
        </optgroup>
      </select>
      <label for="category">Category of Product</label>
      <select id="category" name="category" v-model="selectedCategory">
        <option value="" disabled>--Select a Category--</option>
        <option v-for="category in categories" :key="category.id">{{ category }}</option>
      </select>
      <label for="product">Product</label>
      <select id="product" v-model="selectedProduct">
        <option value="" disabled>--Select a Product--</option>
        <option v-for="product in productList" :key="product.id">{{ product }}</option>
      </select>
      <label for="ratio">Dilution Ratio</label>
      <select id="ratio" v-model="selectedRatio">
        <option value="" disabled>--Choose Dilution Ratio--</option>
        <option v-for="ratio in ratios" :key="ratio.id">{{ '1:' + ratio }}</option>
      </select>
      <label for="price">Price per Case</label>
      <input type="number" id="price" v-model="selectedPrice">

      <button v-if="selectedPrice && selectedRatio" @click="lockItIn">Submit</button>
      <button v-if="selectedPrice && selectedRatio" @click="clearForm">Clear</button>

      <!-- Show Confirmation message if product is successfully added -->
    <transition name="fade">
      <p 
      class="alert"
      v-if="showConfirmation">Product was added to table</p>
    </transition>
    </div>
</div>
</template>

<script>
export default{
  name: 'pick-product',
  props: [''],
  data(){
    return{
      showConfirmation: false,
      // User Selections from Form
      selectedBrand: '',
      selectedCategory: '',
      selectedProduct: '',
      selectedRatio: '',
      selectedPrice: '',
      selectedItems: [],

      // Products Array from JSON fetch
      products: [
        {
          brand: '',
          bottleSize: '',
          bottlesPerContainer: '',
          category: '',
          product: '',
          dilution1: '',
          dilution2: '',      
        }
      ]
    }
  },
  computed: {
    brands() {
      let brands = this.products.map(products => products.brand);
      let mergedBrands = [].concat.apply([], brands);

      // Return unique
      return [...new Set(mergedBrands)];
    },
    categories() {
      let categories = [];
      let filtered = this.products.filter(item => item.brand == this.selectedBrand);

      for (let i = 0; i < filtered.length; i++) {
        categories.push(filtered[i].category);
      }

      return [... new Set(categories)];
    },
    productList() {
      let products = [];
      let filtered = this.products.filter(item => item.brand == this.selectedBrand && item.category == this.selectedCategory);

      for (let i = 0; i < filtered.length; i++) {
        products.push(filtered[i].product);
      }

      return [... new Set(products)];
    },
    ratios() {
      let ratios = [];
      let filtered = this.products.filter(item => item.brand == this.selectedBrand && item.category == this.selectedCategory && item.product == this.selectedProduct);

      for (let i = 0; i < filtered.length; i++) {
        ratios.push(filtered[i].dilution1);
      }

      return [... new Set(ratios)];
    }
  },
  methods:{
    lockItIn() {
      this.selectedItems = {
        selectedBrand: this.selectedBrand,
        selectedCategory: this.selectedCategory,
        selectedProduct: this.selectedProduct,
        selectedRatio: this.selectedRatio,
        selectedPrice: this.selectedPrice
      }
      this.showConfirmation = true;
      console.log(this.selectedItems);
      
      // Send signal to App.vue in order to pass
      // data to ProductTable component
      this.$emit("updateTable", this.selectedItems);
    },
    clearForm() {
      this.selectedBrand = '';
      this.selectedCategory = '';
      this.selectedProduct = '';
      this.selectedRatio = '';
      this.selectedPrice = '';
      this.showConfirmation = false;
    }
  },
  mounted() {
    fetch('products.json')
      .then(response => response.json())
      .then(data => (this.products = data));
  }
}
</script>

<style scoped>
</style>
