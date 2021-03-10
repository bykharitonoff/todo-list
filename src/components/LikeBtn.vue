<template>
    <button type="button" @click="counter++">&hearts; {{ counter }}</button>
</template>

<script>
    export default {
        name: "LikeBtn",
        data: function () {
            return {
                counter: 0
            }
        }
    }
</script>

<style scoped>
    button {
        margin-left: 5px;
    }
</style>