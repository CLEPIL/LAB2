<template>
  <v-container class="form">
    <v-row>
      <v-col>注文一覧</v-col>
      <v-col cols="12">
        <v-data-table :headers="headers" :items="items">
          <template #[`item.delete`]="{ item }">
            <v-btn small color="0" @click="deleteItem(item)">
              承認
            </v-btn>
          </template>
        </v-data-table>
      </v-col>
    </v-row>
    <v-row>
      <router-link to="/edi">
        編集
      </router-link>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      headers: [
        {
          text: 'ID',
          value: 'id'
        },
        {
          text: '野菜',
          value: 'name'
        },
        { text: '数量', value: 'age' },
        { text: '受取日時', value: 'date' },
        {
          text: '削除',
          value: 'delete',
          sortable: false
        }
      ],
      items: [
        {
          id: 1,
          name: 'リーキ',
          age: 33,
          date: '11/11'
        },
        {
          id: 2,
          name: '馬鈴薯',
          age: 42,
          date: '11/12'
        },
        {
          id: 3,
          name: 'とうもろこし',
          age: 10,
          date: '11/13'
        }
      ]
    }
  },
  methods: {
    deleteItem (item) {
      const index = this.items.indexOf(item)
      confirm('この注文を承認しますか？') && this.items.splice(index, 1)
    }
  }
}
</script>

<style>
  .tittle {
    color: #000000;
    text-align: center;
  }
  .form {
    text-align: center;
  }
  .button {
    text-align: center;
  }
</style>
