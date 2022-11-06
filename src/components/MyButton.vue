<template>
    <div>
        <button class="btn" type="submit">
            <slot></slot>
        </button>
    </div>
</template>

<script>
    export default {
    }
</script>

<style lang="scss" scoped>
.btn {
    // width: 90px;
    padding: 0 10px 2px;
    height: 30px;
    color: #1f1f1f;
    background: rgb(244,191,76);
    border: none;
    cursor: pointer;
    font-size: 20px;
    transition: transform 500ms ease;
    border-radius: 10px;
    text-align: center;
}

.btn:hover {
    transform: scale(1.1) translateY(-3px);
}

</style>