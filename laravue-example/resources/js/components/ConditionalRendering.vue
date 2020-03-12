<template>
    <div class="conditional-rendering">
        <div class="block-1" v-if="currentBlock == 1">
            This is block 1
        </div>
        <div class="block-2" v-else-if="currentBlock == 2">
            This is block 2
        </div>
        <div class="block-3" v-else>
            This is block 3
        </div>
        <div>
            <button @click="showBlock(1)">Button 1</button>
        </div>
        <div>
            <button @click="showBlock(2)">Button 2</button>
        </div>
        <div>
            <button @click="showBlock(3)">Button 3</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                currentBlock: 1
            }
        },
        methods: {
            showBlock(number) {
                this.currentBlock = number
            }
        }
    }
</script>

<style lang="scss" scoped>
</style>