<template>
  <div>
    <div>
      <h3>

        {Room X} Quick Actions

      </h3>

      <div class="btn-items">
      
        <Button @btn-click="$emit('toggleshowAddTask')" text="Open All Windows" color="green" />
      
        <Button @btn-click="$emit('toggleshowAddTask')" text="Close All Windows" color="orange" />
      
        <Button @btn-click="$emit('toggleshowAddTask')" text="Delete All Windows" color="red" />
      
        <Button @btn-click="$emit('toggleshowAddTask')" text="Turn on All Heaters" color="green" />
      
        <Button @btn-click="$emit('toggleshowAddTask')" text="Turn off All Heaters" color="orange" />
      
        <Button @btn-click="$emit('toggleshowAddTask')" text="Delete All Heaters" color="red" />
      
      </div>
    </div>
      <div class="widgets">
        <WindowTab />
        <HeaterTab />
      </div>
  </div>
</template>

<script>
import WindowTab from './components/WindowTab'
import HeaterTab from './components/HeaterTab'
import Button from './components/Button'

export default {
  name: 'App',
  components: {
    WindowTab,
    HeaterTab,
    Button,
  }
}

</script>

<style>
.widgets {
  display: flex;
}

.btn-items {
  display: flex;
  margin: 20px 20px;
  border-block: red;
}

h3 {
  margin: 20px 20px;
}
</style>

