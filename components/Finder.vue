<template>
  <form @submit="find" class="form-inline d-flex justify-content-between w-100">
    <div class="form-group mx-sm-3 mb-2 float-left w-50">
      <input
        v-model="name"
        type="text"
        class="form-control w-100"
        id="input-name"
        placeholder="nhập tên diễn viên"
      />
    </div>
    <button type="submit" class="btn btn-primary mx-sm-3 mb-2 float-right">Tìm kiếm</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: ''
    }
  },
  methods: {
    find(e) {
      e.preventDefault()
        // send up to parrent
      if (this.name.length > 0)
        this.$emit('find', this.name)
      this.name = ''
    }
  }
}
</script>

<style>
</style>