<template>
  <div class="card mt-2 mb-2">
    <img class="card-img-top" :src="data.imageUrl" alt="Card image cap" />
    <div class="card-body pb-1">
      <h5 class="card-title">{{data.name}} ({{data.japanName}})</h5>
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item">Sinh: {{data.birthday || '? '}}</li>
      <li class="list-group-item">Cao: {{data.height || '? '}}cm</li>
      <li
        class="list-group-item"
      >3 vòng: {{data.bust || '? '}}-{{data.waist || '? '}}-{{data.hip || '? '}}</li>
    </ul>
    <div class="card-body">
      <a :href="data.siteUrl" target="_blank" class="card-link">Site link</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: ['data']
}
</script>

<style>
</style>