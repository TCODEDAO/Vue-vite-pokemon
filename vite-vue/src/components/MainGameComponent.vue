<template>
    <div class="screen ">
        <div class="screen__inner" :style="{ width: `${widthProp}px` }">
            <PokemonCard v-for="(card, index)  in cardsContext" :clickable="clickable" :ref="`card-${index}`"
                :imgUrlBackFace="`images/${card}.png`" :card="{ card: card, index: index }" :rules="rules"
                @onFlip="checkRule($event)" :key="index" />
        </div>
    </div>
</template>
<script>
import PokemonCard from './PokemonCardComponent.vue'


export default {
    data() {
        return {
            rules: [],
            clickable: true,
        }
    },
    props: {
        cardsContext: {
            type: Array,
            default: () => {
                return []
            }
        },
        widthProp: { type: Number }
    },
    components: {
        PokemonCard: PokemonCard
    },
    methods: {
        checkRule(card) {
            if (this.rules.length === 2) {
                // this.rules.shift()
                return false

            }
            this.rules.push(card)

            // Check double click one card
            if (`card - ${this?.rules[0]?.index}` === `card - ${this?.rules[1]?.index}`) {
                this.clickable = false
                this.rules.pop()
            }


            // Check rule in game
            if (this.rules.length === 2 && this.rules[0].card === this.rules[1].card) {
                this.$refs[`card-${this.rules[0].index}`][0].onEnabledTheDisabledMode()
                this.$refs[`card-${this.rules[1].index}`][0].onEnabledTheDisabledMode()

                this.rules = []
                this.clickable = true

                const totalDisabledElements = document.querySelectorAll('.screen .card.disabled')

                if (totalDisabledElements && totalDisabledElements.length === this.cardsContext.length - 2) {
                    setTimeout(() => {
                        this.$emit('onFinishGame')
                    }, 1500)
                }
            } else if (this.rules.length === 2 && this.rules[0].card !== this.rules[1].card) {
                this.clickable = false
                setTimeout(() => {
                    this.$refs[`card-${this.rules[0].index}`][0].onCloseFlipCard()
                    this.$refs[`card-${this.rules[1].index}`][0].onCloseFlipCard()

                    this.rules = []
                    this.clickable = true
                }, 700)

            } else {
                this.clickable = false
                setTimeout(() => {
                    this.clickable = true
                }, 700)
            }
        }
    }
}
</script>
<style lang="scss" scoped>
@import './../assets/styles/variable.scss';

.screen {
    width: 100%;
    height: 100%;
    z-index: 2;
    background-color: $dark-color;
}

.screen__inner {
    display: flex;
    flex-wrap: wrap;
    padding: 2rem 0;
    margin: auto;
}
</style>