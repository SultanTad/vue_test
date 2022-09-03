<template>
  <div id="app">
    <h1>Добавление товара</h1>
    <div>
        <input type="search" placeholder="поиск" v-model="filter">
    </div>
    <div class="main-products">
      <div class="layout_product">
        <AddContent 
          v-bind:productToEdit="productToEdit"
          @add-product="addProduct"
          @update-product="onUpdateProduct"
        />
      </div>
      <div class="add_products">
        <ItemProduct   
        v-for="product of filteredProducts"
        v-bind:product="product"
        @delete-product="onDelete"
        @edit-product="onEdit"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AddContent from '@/components/AddContent';
import ItemProduct from '@/components/ItemProduct';
export default {
  name: 'App',
  data() {
    return {
      products: [],
      productToEdit: null,
      filter: ""
    };
  },
  computed: {
        filteredProducts: function() {
            return this.products.filter((product) =>{
                return product.title.startsWith(this.filter);
            });
        }
    },
    async mounted() {
      const data = await localStorage.getItem('products')
      data ? this.products = JSON.parse(data) : null
    },
  methods: {
    onDelete(id) {
      let index = this.products.findIndex((p) => p.id === id);
      if (index !== -1) {
        this.products.splice(index, 1);
      }
      localStorage.setItem('products', JSON.stringify(this.products))
    },
    onEdit(id) {
      let index = this.products.findIndex((p) => p.id === id);
      this.productToEdit = this.products[index]
    },
    addProduct(product) {
      this.products.push(product)
      localStorage.setItem('products', JSON.stringify(this.products))
    },
    onUpdateProduct({ id, product }) {
      let index = this.products.findIndex((p) => p.id === id);
      if (index !== -1) {
        this.products.splice(index, 1, product);
      }
      this.productToEdit = null;
    }
  },
  components: {
    AddContent,
    ItemProduct
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.main-products {
  display: flex;
  margin-top: 50px;
}
.add_products {
  margin-left: 30px;
  display: flex;
  flex-wrap: wrap;
}
</style>
