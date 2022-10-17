<template>
    <div class="modal">
      <div class="modal-block">
        <h3 class="modal-block__title">Добавить заметку</h3>
        <div class="modal-block__input">
          <label>
            <span>title</span>
            <input type="text" placeholder="Title" v-model="title">
          </label>
          <label>
            <span>Content</span>
            <textarea placeholder="Content" v-model="content"></textarea>
          </label>
        </div>
        <div class="modal-block__controllers">
          <button class="btn cancel" @click="modalCancel">Отменить</button>
          
          <button v-if="!this.edit" class="btn add" @click="newNote">Добавить</button>
          <button v-else class="btn add" @click="editNote">Изменить</button>
        </div>
      </div>
    </div>
</template>

<script>
  export default {
    name: "modal",
    data(){
      return {
        title: this.edit ? this.editContent.title : '',
        content: this.edit ? this.editContent.content :'',
        error: '',
      }
    },
    props: ['edit','editContent'],
    methods: {
      modalCancel(){
        this.$emit('modalCancel', false)

      },
      newNote(){
        this.$emit('modalCancel', false)
        
        const title = this.title
        const content = this.content
        const date = new Date().toLocaleDateString()
        const newTask = {title, content, date}
        this.$emit('add-item', newTask)
        
        this.title = ''
        this.content = ''
      },
      editNote(){
       this.$emit('modalCancel', false) 
        const newTask = {
          title: this.title, 
          content: this.content,
          date: this.editContent.date,
          id: this.editContent.id
          }
this.$emit('edit-item', newTask)
this.title = '',
this.content = ''
      },
    }
  }
</script>
