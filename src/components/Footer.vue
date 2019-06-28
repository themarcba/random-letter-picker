<template>
    <div class="footer">
        Made with
        <i class="fas fa-heart"></i> by
        <a href="https://marc.dev">Marc Backes</a>
        <div class="footer-icons">
            <a class="info-icon" href="https://github.com/themarcba/random-letter-picker#why">
                <i class="far fa-info-circle"></i>
            </a>
            <a class="gh-icon" href="https://github.com/themarcba/random-letter-picker">
                <i class="fab fa-github"></i>
            </a>
        </div>
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
.footer-icons {
    font-size: 2em;
    position: fixed;
    right: 10px;
    top: 10px;
}

.footer-icons a {
    margin: 5px;
}
.fa-heart {
    color: tomato;
}
</style>
