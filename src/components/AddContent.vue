<template>
    <div>
        <div class="register-cards">
            <div class="product_forms">
                
                <form class="windows_form" @submit.prevent="onSubmit">
                    <p>Наименование товара</p>
                    <input required v-model="product.title" class="name__product" type="text" placeholder="Введите наименование товара">
                    <p>Описание товара</p>
                    <input required v-model="product.description" class="description__product" type="text" placeholder="Введите описание товара">
                    <p>Ссылка на изображение товара</p>
                    <input required v-model="product.link" class="link__product" type="text" placeholder="Введите ссылку">
                    <p>Цена товара</p>
                    <input required v-model="product.price" class="price__product" type="text" placeholder="Введите цену">
                    <button type="submit">{{ submitAction }}</button>
                </form>
                
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        productToEdit: {
            type: Object,
            default: null
        }
    },
    data() {
        return { 
            product: {title: '',
            description: '',
            link: '',
            price: ''}
        }
    },
    computed: {
    submitAction() {
      return this.productToEdit !== null ? "Обновить" : "Добавить товар";
    },
  },
    watch: {
        productToEdit() {
        this.product = { ...this.productToEdit };
        },
    },
    methods: {
        onSubmit() {
            if (this.productToEdit) {
            this.$emit("update-product", {
            id: this.productToEdit.id,
            product: this.product,
        });
      } else {
            this.$emit("add-product", { ...this.product });
            this.product = {};
      }
        }
        
    }
}
</script>

<style scoped>
    .windows_form {
        display: flex;
        flex-direction: column;
    }

    input {
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        border: 0px solid white;
    }
    input:invalid:not(:focus):not(:placeholder-shown) {
        border: 0px solid red;
    }

    .name_product {
        width: 284px;
        height: 36px;
    }

    .description__product {
        width: 284px;
        height: 108px;
    }
    .link__product {
        width: 284px;
        height: 36px;
    }
    .price__product {
        width: 284px;
        height: 36px;
    }
    button {
        margin-top: 24px;
    }
    .register-cards {
        display: flex;
    }

</style>