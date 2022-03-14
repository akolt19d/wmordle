<template>
    <div id="grid-wrapper">
        <div id="grid">
            <div 
                v-for="n in 30" 
                v-bind:key="n" 
                class="grid" 
                :id="'grid' + ((Math.floor((n/5) - 0.01)) + 1).toString() + (n % 5 != 0 ? n % 5 : 5)"
            >
                <!-- {{ n }} -->
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "GameComponent"
}
</script>

<style lang="scss" scoped>

</style>