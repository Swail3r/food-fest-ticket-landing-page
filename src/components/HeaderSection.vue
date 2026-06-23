<template>
  <header class="hero">
    <h1>Cape Town Food Fest 2026</h1>

    <p>
      Enjoy a weekend of food, music,
      and unforgettable experiences.
    </p>
    <div class="controls">
      <label>
        Sort:
        <select @change="$emit('update:sort', $event.target.value)">
          <option value="none">None</option>
          <option value="price-asc">Price: Low → High</option>
          <option value="price-desc">Price: High → Low</option>
        </select>
      </label>

      <label>
        Tier:
        <select @change="$emit('update:filter', $event.target.value)">
          <option>All</option>
          <option>Bronze</option>
          <option>Silver</option>
          <option>Gold</option>
        </select>
      </label>

      <button class="theme-toggle" @click="$emit('toggle-theme')">Toggle Theme</button>
    </div>
  </header>
</template>

<script setup>
const emit = defineEmits(['update:sort', 'update:filter', 'toggle-theme']);
</script>