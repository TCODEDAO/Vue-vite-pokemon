<template>
    <div class="screen"
        style="width: 100%;height: 100vh;background: #282828;display: flex;flex-direction: column;justify-content: center;align-items: center;">
        <h1 style="color:#f3f3f3;font-size: 6vw; margin-bottom:10% ;">POKEMON MEMORIES</h1>
        <h3 style="color:#f3f3f3;font-size: 4vw; margin-bottom:8px;">Chọn cấp độ để bắt đầu</h3>
        <div class=" actions" style="">
            <button @click="onChooseLevel(16)">
                <span>4x4</span>
                <span>Dễ</span>
            </button>
            <button @click="onChooseLevel(36)">
                <span>6x6</span>
                <span>Thường</span>
            </button>
            <button @click="onChooseLevel(64)">
                <span>8x8</span>
                <span>Khó</span>
            </button>
            <button @click="onChooseLevel(100)">
                <span>10x10</span>
                <span>Siêu khó</span>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        onChooseLevel(totalOfBlocks) {
            this.$emit("onChooseLevel", { totalOfBlocks: totalOfBlocks })
        }
    }
}
</script>

<style>
.actions {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
    margin-top: 2rem;
}

.actions button {
    font: var(--font);
    width: 150px;
    height: 150px;
    background: transparent;
    box-shadow: none;
    border: 1px solid #f3f3f3;
    color: #f3f3f3;
    display: flex;
    flex-direction: column;
    border-radius: 1rem;
    margin: 4px 1rem;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: background 0.3s ease-in-out;

}

.actions button:hover {
    background-color: #f3f3f3;
    color: #282828;
}

.actions button span:first-child {
    font-size: 2rem;
}

.actions button span:last-child {
    display: block;
    font-size: 1.25rem;
    margin-top: 0.5rem;
}
</style>