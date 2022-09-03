<template>
    <div>
        <div class="item-cards">
            <div class="card_img">
                <img class="link_img"  :src="product.link">
                <button class="vector_img edit" @click="onEditClick"><img class="edit-img" src="@/assets/Edit_icon-icons.com_71853.svg" alt=""></button>
                <button class="vector_img" @click="onDeleteClick"><img src="@/assets/Vector.svg" alt=""></button>
            </div>
            <div class="card-content">
                <span>{{ product.title }}</span>
                <span>{{ product.description }}</span>
                <span>{{ product.price }}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        product: {
            type: Object,
            required: true
        }
    },
    methods: {
        onDeleteClick() {
            this.$emit('delete-product', this.product.id)
        },
        onEditClick() {
            this.$emit('edit-product', this.product.id)
        }
    }
}
</script>

<style scoped>
    .link_img {
        width: 332px;
        height: 200px;
    }

    .card_img .vector_img {
        display: none;
    }

    .card_img:hover .vector_img {
        display: inline-block;
    }

    .vector_img {
        background-color: red;
    }

    .edit {
        width: 30px;
        height: 30px;
        background-color: #fff;
    }

    .edit-img {
        width: 25px;
        height: 25px;
    }

    .item-cards {
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        width: 332px;
        height: 423px;
        margin-left: 16px;
        margin-bottom: 16px;
    }
    .card-content {
        display: flex;
        flex-direction: column;
        margin-top: 16px;
    }
</style>