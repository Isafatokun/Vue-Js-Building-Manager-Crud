<template>
    <div :key="window.id" v-for="window in windows">

        <Window 
            @toggleStatus="$emit('toggleStatus',window.id)"
            @delete="$emit('delete',window.id)" :window="window" />
    </div>
</template>

<script>
import Window from './Window'

export default {
    name: 'Windows',
    props: {
        windows: Array,
    },
    components: {
        Window
    },    
    emits: ['delete','toggleStatus'],
}
</script>

