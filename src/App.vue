<script setup>
    import HelloWorld from './components/HelloWorld.vue'
    import TheWelcome from './components/TheWelcome.vue'
</script>
<script>
    import { reactive, computed, defineComponent } from 'vue'

    const author = reactive({
        name: 'John Doe',
        books: [
            'Vue 2 - Advanced Guide',
            'Vue 3 - Basic Guide',
            'Vue 4 - The Mystery'
        ]
    })

    // Computed method
    const publishedBooksMessage = computed(() => {
        return author.books.length > 0 ? 'Yes' : 'No'
    })

    export default defineComponent({
        data() {
            return {
                pseudo: '',
                activeColor: 'red',
                fontSize: 24,
                isBig: false,
                isError: true,
                numbers: [1, 2, 3, 4, 5],
                showModal: true,
                login: true,
                username: 'prenom',
                count: 1,
                firstname: 'James',
                lastname: 'Bond',
                languages: ['HTML', 'CSS', 'PHP', 'JS', 'Python'],
                article: {
                    name: "DVD",
                    price: 20
                },
                images: [
            /*        { id: 1, alt: "Un chat dans un arbre", src: "uploads/cat.jpg"},
                    { id: 2, alt: "Un ciel étoilé", src: "uploads/cat.jpg" },
                    { id: 3, alt: "Des enfants qui jouent au foot", src: "uploads/cat.jpg" }*/
                ]
            }
        },
        computed: {
            doubleCount() {
                return this.count * 2
            },
            evenNumbers() {
                return this.numbers.filter(number => number % 2 === 0)
            }
        },
        methods: {
            learningStatus() {
                return this.languages.length >= 5 ? "est confirmé" : "est encore en apprentissage";
            },
            presentation() {
                return `${this.lastname}, ${this.firstname} ${this.lastname}.`;
            },
            increment() {
                this.count++
            },
            addToCart(event) {
                const offers = {
                    1: 1,
                    5: 0.9,
                    10: 0.75
                };
                const number = event.target.value;
                const total = number * this.article.price * offers[number];
                alert(`Vous avez choisi ${number} ${this.article.name}(s) pour ${total}€`);
            }
        },
        watch: {
            count(newValue, oldValue) {
                console.log(`From ${oldValue} to ${newValue}`);
            }
        },
        mounted() {
            // do something when the component is mounted
        }
    })
</script>

<template>
    <header>
        <input type="text" name="pseudo" v-model="pseudo">
        <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">...</div>
        <span class="alert" :class="{ 'alert-big': isBig, 'alert-danger': isError }">
            Mauvais mot de passe
        </span>
        <img v-bind:src="image.src" v-bind:alt="image.alt" v-for="image in images" :key="image.id">
        <img src="{{ image.src }}" alt="{{ image.alt}}" v-for="image in images" :key="image.id">
        <img src="image.src" alt="image.alt" v-for="image in images" :key="image.id">
        <ul>
            <li v-for="item in images" :key="item.id">...</li>
        </ul>
        <ul>
            <li v-for="n in evenNumbers">
                {{ n }}
            </li>
        </ul>
        <button @click="showModal = !showModal">En savoir plus</button>
        <div v-show="showModal" class="modal">...</div>
        <p v-if="login">Bonjour {{ username }}</p>
        <p v-else>Bonjour</p>
        <p>Acheter {{ article.name }} au prix de {{ article.price }}€. Combien en voulez-vous ?</p>
        <select v-on:change="addToCart($event)">
            <option value="1">1</option>
            <option value="5">5 (- 10%)</option>
            <option value="10">10 (- 25%)</option>
        </select>
        <button v-on:click="count++">Cliquez-moi</button>
        <p>Le bouton a été cliqué {{ count }} fois.</p>
        <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
        <span>{{ publishedBooksMessage }}</span>
        <p>{{ presentation() }}</p>
        <p>{{ firstname }} {{ lastname }} {{ learningStatus() }} {{ doubleCount }}.</p>
        <div class="wrapper">
            <HelloWorld msg="You did it!" />
        </div>
    </header>

    <main>
        <TheWelcome />
    </main>
</template>

<style scoped>
    header {
        line-height: 1.5;
    }

    .logo {
        display: block;
        margin: 0 auto 2rem;
    }

    @media (min-width: 1024px) {
        header {
            display: flex;
            place-items: center;
            padding-right: calc(var(--section-gap) / 2);
        }

        .logo {
            margin: 0 2rem 0 0;
        }

        header .wrapper {
            display: flex;
            place-items: flex-start;
            flex-wrap: wrap;
        }
    }
</style>
