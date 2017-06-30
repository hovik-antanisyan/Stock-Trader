<template>
    <div>
        <h1>Trade or view Your Portfolio</h1>
        <h6>You may Save & Load your data</h6>
        <h6>Click on 'End Day' to start e New Day!</h6>
        <hr>
        <p>Your funds: {{ funds | currency}}</p>
    </div>
</template>

<script>
    export default {
        computed: {
            funds() {
                return this.$store.getters.funds;
            }
        }
    }
</script>