<script>
import axios from "axios";
import AppCard from "./components/AppCard.vue";
export default {
  name: 'App',
  data() {
    return {
      cards: [],
    }
  },
  components: {
    AppCard
  },
  methods: {

  },
  mounted() {
    axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
      .then((resp) => {
        const cardsList = resp.data.data;
        console.log(cardsList);
        cardsList.forEach(card => {
          const cardObj = {
            name: card.name,
            archetype: card.archetype,
            img: card.card_images[0].image_url,
          }
          this.cards.push(cardObj)
        });
      })
  },
}
</script>

<template>
  <div class="container">
    <div class="row d-flex f-wrap jf-center">
      <div class="col-3 col-lg-4 col-md-6 col-sm-12" v-for="card in cards">
        <AppCard :img="card.img" :name="card.name" :type="card.archetype"></AppCard>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  background-color: var(--ygo-light);
  padding: 1rem 2rem;
}
</style>