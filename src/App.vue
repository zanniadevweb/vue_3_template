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
                firstname: 'James',
                lastname: 'Bond',
                languages: ['HTML', 'CSS', 'PHP', 'JS', 'Python']
            }
        },
        computed: {
            doubleCount() {
                return this.count * 2
            }
        },
        methods: {
            presentation() {
                return `${this.lastname}, ${this.firstname} ${this.lastname}.`;
            },
            increment() {
                this.count++
            }
        },
        watch: {
            count(newValue, oldValue) {
                // do something when count changes
            }
        },
        mounted() {
            // do something when the component is mounted
        }
    })
</script>

<template>
    <header>
        <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
        <span>{{ publishedBooksMessage }}</span>
        <p>{{ presentation() }}</p>
        <p>{{ firstname }} {{ lastname}} {{ languages.length >= 5 ? "est confirmé" : "est encore en apprentissage" }}.</p>
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
