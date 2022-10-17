<template>
  <div class="container info-setting">
    <h3>Все заметки</h3>
    <button class="info-setting__btn" @click="changeState" v-if="gridOrList">
      <img src="../assets/images/list.svg" alt="">Список
    </button>
    <button class="info-setting__btn" @click="changeState" v-else>
      <img src="../assets/images/grid.svg" alt="">сетка
    </button>


  </div>
</template>


<script>



export default({
name:'info',
props:['title','gridOrList'],
methods: {
  changeState(){
    this.$emit('change-state', !this.gridOrList)
    localStorage.flex = JSON.stringify(!this.gridOrList)
  }
},

})

</script>