<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" id="name" placeholder="Add Window Name" v-model="name" />
        </div>
        
        <div class="form-control form-control-check">
            <label for="status">Choose Status</label>
            <input type="checkbox" id="status" v-model="status" />
        </div>
        <input type="submit" value="Save Window" class="btn btn-block" @click.prevent="onSubmit" />
    </form>
</template>

<script>

export default{
    name : 'AddWindow',
    data() {
        return {
            name: '',
            power: '',
            status: false,
        }
    } ,
    methods : {
        onSubmit(e) {
            e.preventDefault()
            if (!this.name) {
                alert('Please add a Window name')
                return
            }

            const newWindow = {
                name: this.name,
                power: this.power,
                status: this.status,
            }
            
            this.$emit('new-window', newWindow)

            this.name = ''
            this.power = ''
            this.status = 'false'
        }
    } 
}
</script>

<style scoped>
.add-form {
    margin-bottom: 40px;
}

.form-control {
    margin: 20px 0;
}

.form-control label {
    display: block;
}

.form-control input {
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
}

.form-control-check {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.form-control-check label {
    flex: 1;
}

.form-control-check input {
    flex: 2;
    height: 20px;
}
</style>