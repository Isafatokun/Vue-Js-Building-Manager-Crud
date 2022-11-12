<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @btn-click="$emit('toggleshowAddWindow')" 
        
        :text="showAddWindow ? 'Close' : 'Add Window'" 
        
        :color="showAddWindow ? 'red' : 'blue'" 
        />
    </header>
</template>

<script>
import Button from './Button'

 export default {
    name : 'Header',
    props: {
        title: {
            type: String,
        },
        showAddWindow : Boolean,
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