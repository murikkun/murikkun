<template>
  <div class="container navbar-nav" v-if="!search">
    <button class="navbar-nav__lang">uz</button>
    <h2 class="navbar-nav__title">Заметки</h2>
    <button class="navbar-nav__search" @click="searching">
      <img src="../assets/images/search.svg" alt="">
    </button>
  </div>
  
  <div class="container navbar-nav navbar-search" v-else>
    <button class="navbar-search__close" @click="searchClose">
      <img src="../assets/images/back.svg" alt="">
    </button>
    <div class="navbar-search__input">
      <input type="text" placeholder="Поиск..." v-model="searchValue" @input="onInput">
    </div>
    <button class="navbar-search__clear" @click="reset">
      <img src="../assets/images/clear.svg" alt="">
    </button>
  </div>
  
</template>

<script>
export default {

  data(){
    return{
      // search: false
      searchValue: '',
    }
    },
  props: ['search', 'value'],
  methods: {
    searching(){
      this.$emit('update-navbar', !this.search)
    },
    searchClose(){
      this.searchValue = ''
      this.$emit('update-navbar', !this.search)
    },
    reset(){
      this.$emit('value-navbar','',)
      this.searchValue = ''
    },
    onInput(){
      this.$emit('value-navbar', this.searchValue) 
    }
  }
}
</script>