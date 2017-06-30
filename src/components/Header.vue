<template>
    <nav class="navbar navbar-default">
        <div class="container-fluid">
            <div class="navbar-header">
                <router-link class="navbar-brand" to="/">Stock Trader</router-link>
            </div>
            <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                <ul class="nav navbar-nav">
                        <router-link
                                tag="li"
                                activeClass="active"
                                to="/portfolio"
                                :key="'portfolio'"><a>Portfolio</a></router-link>
                        <router-link
                                tag="li"
                                activeClass="active"
                                to="stocks"
                                :key="'stocks'"><a>Stocks</a></router-link>
                </ul>
                <strong class="navbar-text navbar-right">Funds: {{ funds | currency}}</strong>
                <ul class="nav navbar-nav navbar-right">
                    <li><a @click="endDay">End Day</a></li>
                    <li
                            class="dropdown"
                            :class="{open: isOpened}"
                            @click="isOpened = !isOpened">
                        <a
                           class="dropdown-toggle"
                           data-toggle="dropdown"
                           role="button" aria-haspopup="true"
                           aria-expanded="false">Dropdown <span class="caret"></span></a>
                        <ul class="dropdown-menu">
                            <li><a @click="saveData">Save Data</a></li>
                            <li><a @click="loadData">Load Data</a></li>
                        </ul>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<script>
    import {mapActions} from 'vuex';

    export default {
        data() {
            return {
                isOpened: false
            };
        },
        methods: {
            ...mapActions({
                randomizeStocks: 'randomizeStocks',
                fetchData: 'loadData'
            }),
            endDay() {
                this.randomizeStocks();
            },
            saveData() {
                const data = {
                    stocks: this.$store.getters.stocks,
                    stockPortfolio: this.$store.getters.stockPortfolio,
                    funds: this.$store.getters.funds,
                };
                this.$http.put('data.json', data);
            },
            loadData() {
                this.fetchData();
            }
        },
        computed: {
            funds() {
                return this.$store.getters.funds;
            }
        }
    }
</script>

<style scoped>
    a {
        cursor: pointer;
    }

</style>