<template>
    <div 
    @dblclick="$emit('toggleStatus', heater.id)" 
    
    :class="[heater.status ? 'status' : '','heater']">
        
    <h3>
        {{ heater.name }}
        <i @click="$emit('delete', heater.id)" class="fas fa-times">Delete Button</i>
        </h3>
        <p>{{ heater.status }}</p>
    </div>
</template>

<script>

export default {
    name: 'Heater',
    props: {
        heater: Object,
    },
}

</script>


<style>
.fas {
    color: red;
}

.heater {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}

.heater.status {
    border-left: 5px solid green;
}

.heater h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>