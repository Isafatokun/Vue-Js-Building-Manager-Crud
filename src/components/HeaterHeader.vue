<template>
    <header>
        <h1>{{ title }}</h1>
        
        <Button @btn-click="$emit('toggleshowAddHeater')" 
        
        :text="showAddHeater ? 'Close' : 'Add Heater'" 
        
        :color="showAddHeater ? 'red' : 'blue'" 
        />
    </header>
</template>

<script>
import Button from './Button'

 export default {
    name : 'HeaterHeader',
    props: {
        title: {
            type: String,
        },
        showAddHeater : Boolean,
    },
    components: {
        Button
    }
 }
</script>

<style scoped>
    header {
        display : flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>

