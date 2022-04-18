<template>
  <h1>Edit Project</h1>

  <form @submit.prevent="handleUpdate">
    <label>Title:</label>
    <input type="text" v-model="title" required>
    <label>Details:</label>
    <textarea v-model="details" required></textarea>
    <button>Save</button>
  </form>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      uri: 'http://localhost:3000/project/' + this.id
    }
  },
  methods: {
    handleUpdate() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({
          title: this.title,
          details: this.details
        })
      }).then(() => {
        this.$router.push('/')
      }).catch(error => console.log(error))
    }
  },
  mounted() {
    fetch(this.uri)
      .then(response => response.json())
      .then(data => {
        this.title = data.title
        this.details = data.details
      })
      .catch(error => console.log(error))
  }
}

</script>

<style>

</style>