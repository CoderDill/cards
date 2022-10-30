<template>
  <div class="bg-felt h-screen w-screen p-10">
    <div class="flex justify-around">
      <h1>Dealer</h1>
      <h1>Player</h1>
    </div>
    <div class="">
      
        <div class="flex">
          <img :src="cards.cards[0].image" />
          <img :src="cards.cards[1].image" />
        </div>
        <div class="flex">
          <img :src="cards.cards[2].image" />
          <img :src="cards.cards[3].image" />
        </div>
      
    </div>
  </div>
</template>

<script setup>
const { data: newDeck } = await useFetch(
  "https://www.deckofcardsapi.com/api/deck/new/shuffle/?deck_count=2"
);
const deckId = ref(newDeck.value.deck_id);
const { data: cards } = await useFetch(
  `https://www.deckofcardsapi.com/api/deck/${deckId.value}/draw/?count=4`
);

async function drawCard() {
  const { data: drawCard } = await useFetch(
    `https://www.deckofcardsapi.com/api/deck/${deckId.value}/draw/?count=1`
  );
}
</script>
