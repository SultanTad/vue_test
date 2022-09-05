<template>
    <div>
        <select @change="onChange">
            <option value="default">По умолчанию</option>
            <option value="priceUp">{{categories.priceUp}}</option>
            <option value="priceDown">{{categories.priceDown}}</option>
            <option value="title">{{categories.title}}</option>
        </select>
    </div>
</template>

<script>
export default {
    name: 'SelectSort',
    data() {
        return {
            categories: {
                priceUp: 'Цена по возрастанию',
                priceDown: 'Цена по убыванию',
                title: 'В алфавитном порядке'
            }
        }
    },
    methods: {
        onChange(event) {
            this.$emit('sort', event.target.value)
        }
    }
    
}
</script>