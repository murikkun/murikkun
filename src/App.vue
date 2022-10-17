<template>
  <nav class="navbar">
    <navBar 
      :search="search"
      :value="value" 
      @update-navbar="updateNavbar"
      @value-navbar="valueNavbar"
    />
  </nav>
  <section class="info">

    <infoSet
    :gridOrList="this.gridOrList"
    :title="this.search"
    @change-state="changeStateBtn"
    />
  </section>
  <section class="cards">
    <div class="" >
      <div class="container cards-items" v-if="!search" :class ="{list: !gridOrList, grid:gridOrList}">

        <cardItem
          v-for="(item, key) in list" :key="key" 
          :item="item" 
          :i="key"
          :search="this.search"
          @del-item="delItem"
          @edit-item="editItem"
        />
      </div>
      <div class="container cards-items" v-else>
        <cardItem
          v-for="(item, key) in filterList" :key="key" 
          :item="item" 
          :i="key"
        />
      </div>


      
    </div>
  </section>
  <Transition name="scale"> 
    <modalForm 
      v-show="window"
      :edit="edit"
      :window="window"
      :editContent="this.editContent"
      @modalCancel="modalCancel"
      @add-item="addItem"
      @edit-item="editLocalItem"

    />
  </Transition>
  <addBtn @changeModal="window = $event" />
</template>

<script>
  import navBar from './components/navbar';
  import infoSet from './components/info';
  import cardItem from './components/card';
  import modalForm from './components/modal';
  import addBtn from './components/AddButton';
  
  export default {
    components: {navBar,infoSet, cardItem, modalForm, addBtn},
    data(){
      return{
        gridOrList: false,
        search: false,
        modalOpen: false,
        edit: false,
        window: false,
        list: [],
        filterList: [],
        valueSearch: '',
        editContent:{},
    }
      
    },
    methods: {
      modalCancel(bool){
        this.window = bool
        if(!this.window){
          this.edit = false
          this.editContent = {}
        }
      },
      addItem(newTask){
        localStorage.list = localStorage.list ?? "[]"
        const list = JSON.parse(localStorage.list)
        list.unshift(newTask)
        localStorage.list = JSON.stringify(list)
        this.list.unshift(newTask)
      },
      delItem(item){
        this.list.splice(item, 1)
        localStorage.list = JSON.stringify(this.list)
      },
      editItem(item){
        this.edit = this.window = true;
        this.editContent = this.list[item];
        this.editContent.id = item;
      },
      editLocalItem(item){
        this.list[item.id] = item
        localStorage.list = JSON.stringify(this.list)
      },
      changeStateBtn(bool){
        this.gridOrList = bool
        
      },
      updateNavbar(enableSearch){
          this.search = enableSearch
      },
      valueNavbar(valueSearch){
        this.valueSearch = valueSearch
        this.filterList = this.list.filter((val) =>{
          if(val.title.toLowerCase().indexOf(valueSearch.toLowerCase()) !== -1){
            return val
          }
        })
        if(!valueSearch) this.filterList = []
      }
    },
    computed: {},
    created(){
      this.list = JSON.parse(localStorage.list ?? '[]')
      this.gridOrList = JSON.parse(localStorage.flex ?? 'false')
    }
  }
</script>