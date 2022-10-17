<template>
    <div class="card">
      <div class="card-header">
        <h3 class="card-header__title">{{ item.title }}</h3>
        <span class="card-header__date">{{ item.date }}</span>
      </div>
      <div class="card-content">
        <p>{{item.content}}</p>
      </div>
      <div class="card-footer">
        <button class="card-footer__btn edit" @click="editItem">
          <img src="../assets/images/fab.svg" alt="">РЕДАКТИРОВАТЬ
        </button>
        <button class="card-footer__btn del" @click="delItem">
          <img src="../assets/images/trash.svg" alt="">Удалить
        </button>
      </div>
    </div>
</template>

<script>
export default {
  name: 'cards',
  props: ['item', 'i',],
  methods: {
    delItem(){this.$emit('del-item', this.i)},
    editItem(){this.$emit('edit-item', this.i)},
  },
}
</script>
