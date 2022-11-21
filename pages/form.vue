<template>
  <v-app>
    <v-form class="form">
      <v-row>
        <v-col> 野菜 </v-col>
        <v-col> 数量 </v-col>
        <v-col> 受取日 </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-select :items="items" />
        </v-col>
        <v-col>
          <v-text-field />
        </v-col>
        <v-col>
          <v-menu v-model="menu">
            <template #activator="{ on, attrs }">
              <v-text-field
                v-model="text"
                v-bind="attrs"
                label="ここから選択"
                readonly
                clearable
                v-on="on"
              />
            </template>
            <v-date-picker v-model="picker" @input="formatDate(picker)" />
          </v-menu>
        </v-col>
      </v-row>
      <v-row class="button">
        <v-col>
          <v-btn @click="copy(index)">
            フォーム追加
          </v-btn>
        </v-col>
        <v-col>
          <v-btn>
            <router-link to="/comp">
              送信
            </router-link>
          </v-btn>
        </v-col>
      </v-row>
    </v-form>
  </v-app>
</template>
<script>
export default {
  data () {
    return {
      items: ['野菜1', '野菜2', '野菜3'],
      g: ['250', '500', '750', '1000'],
      menu: '',
      text: '',
      picker: '',
      price: '200'
    }
  },
  methods: {
    formatDate (date) {
      if (!date) { return null }
      const [year, month, day] = date.split('-')
      this.text = `${year}/${month}/${day}`
      this.menu = false
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
