<template lang="">
    <div class="card">
        <div class="card__header">
            <slot name="header">
                200 * 100
            </slot>
        </div>

        <div class="card__body">
            <h5>
                <slot name="title">
                    Card title
                </slot>
            </h5>

            <slot name="body">
                <p>A simple card paragraph which can describe what is actually this card is doing here</p>
            </slot>
        </div>

        <div class="card__footer">
            <slot name="footer">
                <button title="More info">More Info!</button>
            </slot>
        </div>
    </div>
</template>

<script setup lang="ts">
    
</script>
<style scoped>
    .card {
        background-color: #fff;
        padding: 0.3em;
        border: 1px solid #ccc;
        width: 200px;
        border-radius: 5px;
        box-shadow: 0 0 8px 5px rgba(0, 0, 0 0.15);
        transition: transform 0.2s;
        margin: 0.4rem;
    }

    .card:hover {
        transform: scale(1.02);
    }

    .card__header {
        width: 100%;
        aspect-ratio: 3 / 2;
        background-color: rgb(230, 215, 250);
        border-radius: 5px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 2rem;
        font-weight: bold;
    }

    .card__body {
        width: 100%;
        padding: 0.2rem;
        color: #081d20;
    }

    .card__body h5 {
        font-size: 1.3rem;
        margin-top: 0.5rem;
        text-align: left;
        margin-bottom: 0.6rem;
    }

    .card__body p {
        font-size: 0.9rem;
        margin-top: 0;
        text-align: left;
        font-weight: 400;
    }

    .card__footer {
        width: 100%;
    }

    .card__footer button {
        font-size: 0.9rem;
    }
</style>