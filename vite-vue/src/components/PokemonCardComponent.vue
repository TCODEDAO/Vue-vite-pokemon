<template>
    <div class="card" :class="{ disabled: isDisabled }">
        <div class="card-inner" :class="{ 'is-flipped': isFlipped }" @click="handleToggleFlipCard">
            <div class="card-face card-front">
                <div class="card-content"></div>
            </div>
            <div class="card-face card-back">
                <div class="card-content" :style="{ backgroundImage: `url(${('/src/assets/' + imgUrlBackFace)}) ` }">
                </div>
            </div>
        </div>
        <svg class="animated-no-check" :class="{ 'animated-check': isDisabled }" viewBox="0 0 24 24">
            <path d="M4.1 12.7L9 17.6 20.3 6.3" fill="none" />
        </svg>
    </div>
</template>
<script>
export default {
    props: {
        imgUrlBackFace: {
            type: String,
            required: true,
        },
        card: {
            type: [String, Number, Object, Array]
        },
        rules: {
            type: Array,
        },
        clickable: {
            type: Boolean,
        }
    },
    data() {
        return {
            isFlipped: false,
            isDisabled: false,
        }
    },
    methods: {
        onCloseFlipCard() {
            if (this.isDisabled) {
                return false
            }
            this.isFlipped = false
        },
        handleToggleFlipCard() {
            if (this.rules.length >= 2) {
                return false
            }
            if (this.isDisabled) {
                return false
            }
            if (this.clickable) {
                this.isFlipped = !this.isFlipped

                if (this.isFlipped) {
                    this.$emit("onFlip", this.card)
                }

            }

        },
        onEnabledTheDisabledMode() {
            this.isDisabled = true
        }
    }
}
</script>
<style lang="scss" scoped>
@import './../assets/styles/index.scss';
</style>