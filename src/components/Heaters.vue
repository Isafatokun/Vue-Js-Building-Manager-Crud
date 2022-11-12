<template>
    <div :key="heater.id" v-for="heater in heaters">

        <Heater 
            @toggleStatus="$emit('toggleStatus',heater.id)"  
            @delete="$emit('delete',heater.id)" :heater="heater" />
    </div>
</template>

<script>
import Heater from './Heater'

export default {
    name: 'Heaters',
    props: {
        heaters: Array,
    },
    components: {
        Heater
    },
    emits: ['delete', 'toggleStatus'],
}
</script>

