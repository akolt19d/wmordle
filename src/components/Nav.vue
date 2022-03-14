<template>
    <nav>
        <div class="help-wrapper" @click="toggle">?&#191;</div>
        <h1 class="headline-wrapper">Wmordle</h1>
        <div class="settings-wrapper">bruh</div>
    </nav>
</template>

<script>
export default {
    name: "NavComponent",
    methods: {
        toggle() {
            this.$emit('toggle')
        }
    }
}
</script>

<style lang="scss" scoped>
.help-wrapper
{
    cursor: pointer;
    font-weight: bold;
}
</style>