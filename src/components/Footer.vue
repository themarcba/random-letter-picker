<template>
    <div class="footer">
        Made with
        <i class="fas fa-heart"></i> by
        <a href="https://marc.dev">Marc Backes</a>
        <br>
        <a class="gh-icon" href="https://github.com/themarcba/random-letter-picker">
            <i class="fab fa-github"></i>
        </a>
    </div>
</template>

<script>
export default {
    name: "Footer"
};
</script>

<style>
.footer {
    position: fixed;
    width: 100%;
    bottom: 0;
    padding: 0;
}
.gh-icon {
    font-size: 2em;
    position: fixed;
    right: 10px;
    width: 41px;
    bottom: 10px;
}
.fa-heart {
    color: tomato;
}
</style>
