<template>
    <div id="app">
        <RandomLetter></RandomLetter>

        <div class="center">
            <a href="https://github.com/themarcba/random-letter-picker#why">
                <i class="far fa-info-circle"></i>
                Find out what this app is used for
            </a>
        </div>

        <Footer></Footer>
    </div>
</template>

<script>
import RandomLetter from "./components/RandomLetter.vue";
import Footer from "./components/Footer.vue";

export default {
    name: "app",
    components: {
        RandomLetter,
        Footer
    }
};
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}
body {
    margin: 0;
}
div.centered {
    text-align: center;
}

a {
    color: #2ecc71;
    text-decoration: none;
    font-weight: bold;
    -webkit-transition: color 0.3s ease-out;
    -moz-transition: color 0.3s ease-out;
    -o-transition: color 0.3s ease-out;
    transition: color 0.3s ease-out;
}

a:hover {
    color: #2c3e50;
}
</style>
