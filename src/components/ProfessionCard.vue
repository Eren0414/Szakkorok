<template>
  <div class="card card-border-dark">
    <div class="card-header">{{ szakkor.nev }}</div>
    <div class="card-body text-dark mb-2">
      <span 
        class="my-span" 
        v-for="(tanulo, index) in szakkorTanuloi" 
        :key="tanulo.id">
        {{ tanulo.nev }}<span v-if="index < szakkorTanuloi.length - 1">, </span>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    "szakkor",
    "tanulok"
  ],
  computed: {
    szakkorTanuloi() {
      return this.tanulok
        .filter((t) => t.szakkorId == this.szakkor.id)
        .sort((a, b) => a.nev.localeCompare(b.nev));
    }
  }
}
</script>

<style scoped>
.my-span {
  color: white;
}
</style>
