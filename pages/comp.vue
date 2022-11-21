<template>
  <v-container class="comp">
    <v-row>
      <v-col> 送信完了 </v-col>
    </v-row>
    <v-row>
      <v-col>
        <router-link to="/form">
          別の注文
        </router-link>
      </v-col>
    </v-row>
    <v-row>
      <v-col>注文履歴</v-col>
      <v-col cols="12">
        <v-data-table :headers="headers" :items="items" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      headers: [
        { text: '注文日時', value: 'day' },
        { text: '野菜', value: 'name' },
        { text: '数量', value: 'age' },
        { text: '状態', value: 'now' }
      ],
      items: [
        {
          day: '11/8',
          name: 'リーキ',
          age: 33,
          now: '未受取'
        },
        {
          day: '11/7',
          name: '馬鈴薯',
          age: 42,
          now: '受取済'
        },
        {
          day: '11/5',
          name: 'とうもろこし',
          age: 10,
          now: '受取済'
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
.comp {
  text-align: center;
}
.button {
  text-align: center;
}
</style>
