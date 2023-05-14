<template>
  <div>
    <div class="product" v-for="(product, index) in displayedProducts" :key="index">
      <div class="product-img">
        <img :src="product.image" alt="product" />
      </div>
      <div class="product-info">
        <div class="container">
          <h3>{{ product.title }}</h3>
          <p>Price: ${{ product.price }}</p>
          <p>Category: {{ product.category }}</p>
        </div>
      </div>
    </div>

    <div class="pagination">
      <button v-if="currentPage > 1" @click="prevPage">Prev</button>
      <button v-if="currentPage < totalPages" @click="nextPage">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",
  data() {
    return {
      products: [],
      currentPage: 1,
      itemsPerPage: 1,
    };
  },
  created() {
    this.fetchProducts();
  },
  computed: {
    displayedProducts() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.products.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.products.length / this.itemsPerPage);
    },
  },
  methods: {
    fetchProducts() {
      fetch("https://fakestoreapi.com/products")
        .then((response) => response.json())
        .then((data) => (this.products = data));
    },
    prevPage() {
      this.currentPage -= 1;
    },
    nextPage() {
      this.currentPage += 1;
    },
  },
};
</script>

<style scoped>
.product {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-bottom: 50px;
}

.product-img {
  flex-basis: 30%;
}

.product-img img {
  width: 100%;
}

.product-info {
  flex-basis: 68%;
}

.pagination {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

button:disabled {
  background-color: gray;
  cursor: not-allowed;
}
</style>
