<template>
    <div>
      <div class="input-group mb-3">
          <div class="input-group-prepend">
             <span class="input-group-text">名前入れろ</span>
          </div>
          <input
            type="text"
            name="inputUser"
            class="form-control"
            v-model="userName"
            v-on:change="addUser"
            placeholder="入力後enter押してね"
          >
      </div>
    </div>
</template>

<script>
import {_} from 'vue-underscore'

export default {
  name: 'InputUser',
  data () {
    return {
      userName: ''
    }
  },
  methods: {
    addUser () {
      if (!this.userName.length) {
        return
      }
      const users = this.$store.state.users
      const duplicateUser = _.findWhere(users, {name: this.userName})
      if (duplicateUser) {
        this.$store.commit('setModalMessage', '重複だめ絶対')
        return
      }
      this.$store.commit('addUser', this.userName)
      this.userName = ''
      this.$store.commit('updateUserPayments2')
    }
  }
}
</script>

<style scoped lang="scss">
</style>
