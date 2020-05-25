<template>
  <div>
    <button type="info" @click="signOut">退出</button>
  </div>
</template>

<script>
export default {
  methods: {
    signOut() {
      window.sessionStorage.clear()
      this.$router.push('/login')
    }
  }
}
</script>
