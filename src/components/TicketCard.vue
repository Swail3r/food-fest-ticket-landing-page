<template>
  <div
    class="card"
    :class="{ featured: ticket.featured, hovering: hovering }"
    @mouseenter="hovering = true"
    @mouseleave="hovering = false"
  >
    <h2>{{ ticket.name }}</h2>

    <h3 class="price">R{{ ticket.price }}</h3>

    <p>{{ ticket.description }}</p>

    <ul>
      <li
        v-for="benefit in ticket.benefits"
        :key="benefit"
      >
        {{ benefit }}
      </li>
    </ul>

    <div class="card-actions">
      <button class="cta" @click="$emit('buy', ticket)">Buy Now</button>

      <button
        class="favourite-btn"
        :class="{ favourited: favourite }"
        @click="toggleFavourite"
        :aria-pressed="favourite"
      >
        <span class="icon">{{ favourite ? '❤️' : '🤍' }}</span>
        <span class="label">{{ favourite ? 'Favourite' : 'Favourite' }}</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  ticket: Object
});

const favourite = ref(false);
const hovering = ref(false);

const toggleFavourite = () => {
  favourite.value = !favourite.value;
  // simple visual pulse when favourited
  if (favourite.value) {
    setTimeout(() => {}, 200);
  }
};
</script>

<style scoped>
.card {
  --s: 1;
  --ty: 0px;
  transition: transform 180ms ease, box-shadow 180ms ease;
  transform: translateY(var(--ty)) scale(var(--s));
}
.card.hovering {
  --ty: -6px;
  --s: 1.01;
  box-shadow: 0 8px 24px rgba(0,0,0,0.18);
}
.card.featured {
  --s: 1.05;
}
.card.featured.hovering {
  --s: 1.08;
  --ty: -8px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.22);
}
.price {
  color: var(--price-color, #111);
}
.card-actions {
  display: flex;
  gap: 10px;
  align-items: center;
  margin-top: 18px;
  flex-wrap: wrap;
}
.cta {
  background: var(--cta-bg, #ff7a00);
  color: #fff;
  border: none;
  padding: 12px 16px;
  border-radius: 14px;
  cursor: pointer;
  transition: transform 120ms ease, box-shadow 120ms ease, opacity 120ms ease;
  box-shadow: 0 10px 22px rgba(255,138,90,0.22);
}
.cta:hover {
  transform: translateY(-3px);
  box-shadow: 0 14px 28px rgba(255,138,90,0.3);
  opacity: 0.97;
}
.favourite-btn {
  background: rgba(255,255,255,0.2);
  border: 1px solid rgba(255,255,255,0.18);
  padding: 10px 12px;
  border-radius: 14px;
  cursor: pointer;
  display: flex;
  gap: 8px;
  align-items: center;
  transition: transform 160ms ease, background 160ms ease, border-color 160ms ease;
  color: var(--text);
}
.favourite-btn:hover {
  transform: translateY(-1px);
  background: rgba(255,255,255,0.32);
}
.favourite-btn .icon { transition: transform 160ms ease; }
.favourite-btn .label { color: var(--text); }
.favourite-btn.favourited {
  background: linear-gradient(135deg, rgba(255,149,128,0.16), rgba(255,218,143,0.18));
  border-color: rgba(255,149,128,0.28);
  color: var(--text);
}
.favourite-btn.favourited .icon {
  transform: scale(1.2);
}
</style>