<script>
import axios from "axios";
import AppFilter from "./AppFilter.vue";
import AppCard from "./AppCard.vue";
export default {
    name: "AppMain",
    data() {
        return {
            info: [],
            cards: [],
            options: ["All"],
            loading: true,
            apiLInk: `https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0`,
            previousDisable: true,
            nextDisable: false,
        }
    },
    components: {
        AppCard,
        AppFilter
    },
    methods: {
        getCardEl(apiLInk) {
            axios.get(apiLInk)
                .then((resp) => {
                    const cardsList = resp.data.data;
                    console.log(cardsList);
                    cardsList.forEach(card => {
                        const cardObj = {
                            name: card.name,
                            archetype: card.archetype,
                            img: card.card_images[0].image_url_small,
                        }
                        this.info = resp.data.meta;
                        this.cards.push(cardObj);
                        this.loading = false;
                        if (card.archetype == undefined) {
                            card.archetype = "unknown"
                        };
                        if (!this.options.includes(card.archetype)) {
                            this.options.push(card.archetype);
                        };
                    });
                });
        },
        nextPage() {
            if (this.info.pages_remaining != 0) {
                this.cards = [];
                this.loading = true;
                this.getCardEl(this.info.next_page);
            }
            setTimeout(() => {
                if (this.info.pages_remaining != 0) {
                    this.nextDisable = false;
                    this.previousDisable = false;
                } else {
                    this.nextDisable = true;
                };
            }, 1000);
        },
        previousPage() {
            if (this.info.pages_remaining != this.info.total_pages) {
                this.cards = [];
                this.loading = true;
                this.getCardEl(this.info.previous_page);
            };
            setTimeout(() => {
                if (this.info.pages_remaining != this.info.total_pages) {
                    this.nextDisable = false;
                    this.previousDisable = false;
                } else {
                    this.previousDisable = true;
                };
            }, 1000);
        },
    },
    created() {
        this.getCardEl(this.apiLInk);
    }
}
</script>

<template>
    <main>
        <div class="container">
            <AppFilter :options="options"></AppFilter>
            <div class="row d-flex f-wrap jf-center bg-light">
                <div v-if="!loading" class="col-3 col-lg-4 col-md-6 col-sm-12" v-for="card in cards">
                    <AppCard :img="card.img" :name="card.name" :type="card.archetype"></AppCard>
                </div>
                <div v-else>
                    <i class="fa-solid fa-spinner fa-spin-pulse"></i>
                </div>
            </div>
            <div class="row d-flex al-center jf-center bg-light my-3 gap-5">
                <button class="btn" :class="{ disable: previousDisable }" @click="previousPage">previous page</button>
                <button class="btn" :class="{ disable: nextDisable }" @click="nextPage">next page</button>
            </div>
        </div>
    </main>
</template>

<style scoped>
.disable {
    background-color: var(--ygo-disable);
    cursor: default;
}
</style>