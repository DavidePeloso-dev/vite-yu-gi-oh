<script>
import axios from "axios";
import AppFilter from "./AppFilter.vue";
import AppCard from "./AppCard.vue";
export default {
    name: "AppMain",
    data() {
        return {
            cards: [],
            options: ["All"],
        }
    },
    components: {
        AppCard,
        AppFilter
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
                    if (card.archetype == undefined) {
                        card.archetype = "unknown"
                    }
                    if (!this.options.includes(card.archetype)) {
                        this.options.push(card.archetype);
                    };
                });
            })
    },
}
</script>

<template>
    <div class="container">
        <AppFilter :options="options"></AppFilter>
        <div class="row d-flex f-wrap jf-center bg-light">
            <div class="col-3 col-lg-4 col-md-6 col-sm-12" v-for="card in cards">
                <AppCard :img="card.img" :name="card.name" :type="card.archetype"></AppCard>
            </div>
        </div>
    </div>
</template>

<style scoped></style>