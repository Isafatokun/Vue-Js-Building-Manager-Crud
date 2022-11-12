<template>
  <div class="container">
    <Header 
    
    @toggleshowAddWindow="toggleAddWindow"
    title="Window Manager" 
    
    :showAddWindow="showAddWindow" />
    
    <div v-if="showAddWindow">
      <AddWindow @new-window="addWindow" />
    </div>
    
    <Windows 
      @toggleStatus="toggleStatus"
      @delete="deleteWindow" :windows="windows" />
  </div>
</template>

<script>
import Header from './Header'
import Windows from './Windows'
import AddWindow from './AddWindow'

export default {
  name: 'App',
  components: {
    Header,
    Windows,
    AddWindow
  },
  data() {
    return {
      windows: [],
      showAddWindow : false,
    }
  },

  methods: {
    toggleAddWindow() {
      this.showAddWindow = !this.showAddWindow
    },   

    async addWindow(window) {
      const response = await fetch('api/windows', {
        method: 'POST',
        headers: {
          'Content-type' : 'application/json',
        },
        
        body: JSON.stringify(window),      
      
      })

      const data = await response.json()

      this.windows = [...this.windows, data]
    },

    async deleteWindow(id) {
      if (confirm('Are you Sure?')) {
        const response = await fetch(`api/windows/${id}`, {
          method: 'DELETE',
        })

        response.status() === 200 
          ? (this.windows = this.windows.filter(
            (window) => window.id !== id))
             : alert('Error Deleting Window') 

        this.windows = this.fetchWindow()
      }
    },

    async toggleStatus(id) {
      const windowToToggle = await this.fetchWindow(id)

      const updWindow = {...windowToToggle, status: !windowToToggle.status}

      const response = await fetch(`api/windows/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updWindow),
      })

      const data = await response.json()

      this.windows = this.windows.map((window) => 
        window.id === id ? {...window, status: data.status } : window
        )
    }, 

    async fetchWindows() {
      const response = await fetch('api/windows')

      const data = await response.json()

      return data
    },

    async fetchWindow(id) {
      const response = await fetch(`api/windows/{id}`)

      const data = await response.json()

      return data
    }
  },

  async created() {
    this.windows = await this.fetchWindows()
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
