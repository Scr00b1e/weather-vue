<template>
    <div v-if="cityInfo != null">
        {{ cityInfo.name }}
        324 celcium
        rainy
    </div>
</template>

<script>
export default {
    props: {
        type: Object,
        required: true
    }
}
</script>

<style scoped></style>