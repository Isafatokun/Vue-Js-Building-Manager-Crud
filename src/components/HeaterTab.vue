<template>
  <div class="container">
    <HeaterHeader 
    
    @toggleshowAddHeater="toggleAddHeater" 
    title="Heaters" 
    
    :showAddHeater="showAddHeater" />

    <div v-if="showAddHeater">
      <AddHeater @new-heater="addHeater" />
    </div>

    <Heaters 
    @toggleStatus="toggleStatus" 
    @delete="deleteHeater" :heaters="heaters"/>
  </div>
</template>

<script>
import HeaterHeader from './HeaterHeader'
import Heaters from './Heaters'
import AddHeater from './AddHeater'

export default {
  name: 'App',
  components: {
    HeaterHeader,
    Heaters,
    AddHeater
  },
  data() {
    return {
      heaters: [],
      showAddHeater: false,
    }
  },

  methods: {
    toggleAddHeater() {
      this.showAddHeater = !this.showAddHeater
    },

    async addHeater(heater) {
      const response = await fetch('api/heaters', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },

        body: JSON.stringify(heater),

      })

      const data = await response.json()

      this.heaters = [...this.heaters, data]
    },

    async deleteHeater(id) {
      if (confirm('Are you Sure?')) {
        const response = await fetch(`api/heaters/${id}`, {
          method: 'DELETE',
        })

        response.status() === 200
          ? (this.heaters = this.heaters.filter(
            (heater) => heater.id !== id))
          : alert('Error Deleting Heater')

        this.heaters = this.fetchHeater()
      }
    },

    async toggleStatus(id) {
      const heaterToToggle = await this.fetchHeater(id)

      const updHeater = {...heaterToToggle, reminder: !heaterToToggle.reminder }

      const response = await fetch(`api/heaters/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updHeater),
      })

      const data = await response.json()

      this.heaters = this.heaters.map((heater) =>
        heater.id === id ? {...heater, status: data.status } : heater
      )
    },

    async fetchHeaters() {
      const response = await fetch('api/heaters')

      const data = await response.json()

      return data
    },

    async fetchHeater(id) {
      const response = await fetch(`api/heaters/{id}`)

      const data = await response.json()

      return data
    }
  },

  async created() {
    this.heaters = await this.fetchHeaters()
  },
}

</script>
 <!-- lang="scss" -->
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:hover {
  opacity: 80%;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
