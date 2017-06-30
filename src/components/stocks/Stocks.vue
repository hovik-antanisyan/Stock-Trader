<template>
    <div>
        <app-stock v-for="stock in stocks" :stock="stock" :key="stock"></app-stock>
    </div>
</template>

<script>
    import Stock from './Stock.vue';

    export default {
        data() {
            return {
                data: []
            }
        },
        components: {
            appStock: Stock
        },
        computed: {
            stocks() {
                return this.$store.getters.stocks;
            }
        }
    }
</script>