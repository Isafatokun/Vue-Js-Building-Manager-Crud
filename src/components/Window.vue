<template>
    <div 
        @dblclick="$emit('toggleStatus', window.id)"
        
        :class="[window.status ? 'status' : '','window']">
        
        <h3>
            {{ window.name }} 
            <i @click="$emit('delete',window.id)" class="fas fa-times">Delete Button</i>
        </h3>
        <p>{{ window.status }}</p>
    </div>
</template>

<script>

export default {
    name: 'Window',
    props: {
        window: Object,
    },
}

</script>


<style>
.fas {
    color: red;
}

.window {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}

.window.status {
    border-left: 5px solid green;
}

.window h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>