<template>
  <HeaderSection
    @update:sort="(val) => sortOption.value = val"
    @update:filter="(val) => filterTier.value = val"
    @toggle-theme="toggleTheme"
  />

  <div class="tickets">
    <TicketCard
      v-for="ticket in visibleTickets"
      :key="ticket.id"
      :ticket="ticket"
      @buy="handleBuy"
    />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import HeaderSection from "./components/HeaderSection.vue";
import TicketCard from "./components/TicketCard.vue";
import tickets from "./data/tickets";

const sortOption = ref('none');
const filterTier = ref('All');

const visibleTickets = computed(() => {
  let list = tickets.slice();
  if (filterTier.value && filterTier.value !== 'All') {
    list = list.filter(t => t.name === filterTier.value);
  }
  if (sortOption.value === 'price-asc') {
    list.sort((a,b) => a.price - b.price);
  } else if (sortOption.value === 'price-desc') {
    list.sort((a,b) => b.price - a.price);
  }
  return list;
});

const handleBuy = (ticket) => {
  // Placeholder: open purchase flow or notify
  alert(`Buy clicked: ${ticket.name} — R${ticket.price}`);
};

const toggleTheme = () => {
  const body = document.body;
  body.classList.toggle('dark');
  // persist
  localStorage.setItem('theme', body.classList.contains('dark') ? 'dark' : 'light');
};

onMounted(() => {
  const saved = localStorage.getItem('theme');
  if (saved === 'dark') document.body.classList.add('dark');
});
</script>