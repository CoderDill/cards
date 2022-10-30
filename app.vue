<template>
  <div class="flex flex-col bg-felt h-screen w-full p-10">
    <h1 class="">Blackjack</h1>
    <div class="justify-center">
      <h1 class="">Dealer</h1>
      <div class="flex flex-row justify-center gap-3 dealer">
        <template class="" v-for="(card, index) in dealersCards">
          <img class="flex max-h-[200px] max-w-[150px] gap-3" v-if="(index === 1 && backOfCard)"
            src="./assets/back.png" />
          <img class="flex max-h-[200px] max-w-[150px] gap-3" v-else :src="card.image" />
        </template>
      </div>
      <h1>Player</h1>
      <div class="flex flex-row justify-center gap-3" >
        <div v-for="(card, index) in playersCards" class="">
            <img class="flex max-h-[200px] max-w-[150px] gap-3" :key="index" :src="card.image" />
        </div>
      </div>
      <div class="flex justify-evenly">
        <button @click="drawCard" class="border rounded bg-white w-20 h-10 m-5">Hit</button>
        <button class="border rounded bg-white w-20 h-10 m-5">Stand</button>
        <button class="border rounded bg-white w-20 h-10 m-5">Double</button>
        <button class="border rounded bg-white w-20 h-10 m-5">Split</button>
      </div>

    </div>
  </div>
</template>

<script setup>
const backOfCard = ref(true)
const dealersCards = ref([])
const playersCards = ref([])

const { data: newDeck } = await useFetch(
  "https://www.deckofcardsapi.com/api/deck/new/shuffle/?deck_count=2"
);
const deckId = ref(newDeck.value.deck_id);
const { data: cards } = await useFetch(
  `https://www.deckofcardsapi.com/api/deck/${deckId.value}/draw/?count=4`
);
dealersCards.value.push(cards.value.cards[0])
dealersCards.value.push(cards.value.cards[1])
playersCards.value.push(cards.value.cards[2])
playersCards.value.push(cards.value.cards[3])

async function drawCard() {
  const { data: drawCard } = await useFetch(
    `https://www.deckofcardsapi.com/api/deck/${deckId.value}/draw/?count=1`
  );
  playersCards.value.push(drawCard.value.cards[0])
}
</script>
