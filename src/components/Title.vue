<script setup lang="ts">

defineProps({
    size: { type: Number, default: 12 },
    color: { type: String, default: '#00000' },
    title: { type: String, default: 'Sample Title' },
});

</script>

<template>
    <div class="title" :style="{ fontSize: size / 16 + 'rem', color: color }">
        {{ title }}
    </div>
</template>

<style scoped lang="scss">
.title {
    display: flex;
    align-items: center;
}
</style>
