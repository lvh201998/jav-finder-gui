<template>
  <div class="row">
    <div class="col-12 justify-content-between">
      <form @submit="find">
        <div class="input-group input-group-lg">
          <input
            v-model="name"
            type="text"
            class="form-control"
            id="input-name"
            placeholder="nhập tên diễn viên"
          />
          <div class="input-group-btn input-group-append">
            <button type="submit" class="btn btn-primary">Tìm kiếm</button>
          </div>
        </div>
      </form>
    </div>
  </div>
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
      if (this.name.length > 0) this.$emit('find', this.name)
    }
  }
}
</script>

<style>
</style>