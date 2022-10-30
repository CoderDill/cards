<template>
  <div class="bg-felt h-screen w-screen p-10">
        <img :src="cards.cards[0].image" />
  </div>
</template>

<script setup>

const { data: cards } = await useFetch('https://www.deckofcardsapi.com/api/deck/new/draw/?count=2')
</script>
