<template>
    <div class="event-handling">
        <input @keyup.enter="alertHello">

        <input @keyup.13="alertHello">
    </div>
</template>

<script>
    export default {
        methods: {
            alertHello() {
                alert('Hello')
            }
        }
    }
</script>

<style lang="scss" scoped>
</style>