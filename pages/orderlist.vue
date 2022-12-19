<template>
  <v-container>
    <v-row>
      <v-col>注文一覧</v-col>
      <v-col cols="12">
        <v-data-table :headers="headers" :items="items">
          <template #[`item.link`]="{ item }">
            <v-btn :href="item.link">
              連絡
            </v-btn>
          </template>
          <template #[`item.delete`]="{ item }">
            <v-btn small color="0" @click="approvalItem(item)">
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
import { getDatabase, ref, child, get } from 'firebase/database'
export default {
  data () {
    return {
      headers: [
        { text: 'ID', value: 'id' },
        { text: '野菜', value: 'yasai' },
        { text: '数量', value: 'weight' },
        { text: '受取日時', value: 'date' },
        { text: '連絡', value: 'link' },
        { text: '', value: 'delete', sortable: false }
      ],
      items: [
      ]
    }
  },
  mounted () {
    // eslint-disable-next-line no-console
    const dbRef = ref(getDatabase())
    get(child(dbRef, 'orders')).then((snapshot) => {
      if (snapshot.exists()) {
        // eslint-disable-next-line no-console
        console.log(snapshot.val())
        const orders = snapshot.val()
        Object.keys(orders).forEach(k => this.items.push(orders[k]))
      } else {
        // eslint-disable-next-line no-console
        console.log('No data available')
      }
    }).catch((error) => {
      // eslint-disable-next-line no-console
      console.error(error)
    })
  },
  methods: {
    filter (val, search) {
      return val === search
    },
    approvalItem (item) {
      const index = this.items.indexOf(item)
      const result = confirm('この注文を承認しますか？')
      if (result) {
        // eslint-disable-next-line no-console
        console.log('OKがクリックされました')
        this.items.splice(index, 1)
      } else {
        // eslint-disable-next-line no-console
        console.log('キャンセルがクリックされました')
      }
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
