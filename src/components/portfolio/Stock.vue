<template>
    <div class="col-md-4 col-sm-6">
        <div class="panel panel-info">
            <div class="panel-heading">
                <h2 class="panel-title">
                    {{ stock.name }}
                    <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
                </h2>
            </div>
            <div class="panel-body">
                <div class="pull-left">
                    <input
                            type="number"
                            class="form-control"
                            placeholder="Quantity"
                            :class="{danger: insufficientQuantity}"
                            v-model="quantity">
                </div>
                <div class="pull-right">
                    <button
                            class="btn btn-success"
                            @click.prevent="onSellStock"
                            :disabled="insufficientQuantity || quantity <=0 || !Number.isInteger(+quantity)">
                        {{ insufficientQuantity ? 'Not Enough' : 'Sell' }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import {mapActions} from 'vuex';

    export default {
        props: ['stock'],
        data() {
            return {
                quantity: 0
            }
        },
        computed: {
            funds() {
                return this.$store.getters.funds;
            },
            insufficientQuantity() {
                return this.quantity > this.stock.quantity;
            }
        },
        methods: {
            ...mapActions([
                'sellStock'
            ]),
            onSellStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };
                console.log(order);
                this.sellStock(order);
                this.quantity = 0;
            }
        }
    }
</script>

<style scoped="">
    .danger {
        border: 1px red solid;
    }
</style>

