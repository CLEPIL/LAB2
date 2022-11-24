<template>
  <div>
    使い方をここに書く？
  </div>
</template>

<script>
import { getDatabase, ref, set } from 'firebase/database'
export default {
  data () {
    return {
      count: 0,
      age: 30
    }
  },
  mounted () {
  },
  methods: {
    watchdb () {
      const database = getDatabase()
      // eslint-disable-next-line no-console
      console.log(database)
    },
    writeUserData (age) {
      const db = getDatabase()
      set(ref(db), {
        aage: age
      })
    }
  }
}
</script>

<style>

</style>
