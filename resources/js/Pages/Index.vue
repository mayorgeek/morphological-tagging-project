<script setup>
import {Head} from "@inertiajs/vue3";
import {ref} from "vue";

const verbs = ['ba', 'be', 'bo', 'da', 'de', 'go', 'gbe', 'gbo', 'ja', 'jo', 'ke', 'le', 'mi', 'mo', 'nu', 'pa', 'p', 'ra', 'so', 'sa', 'ta', 'wo', 'ya', 'ye', 'yo'];
const vowels = ['a','e','i','o','u'];
const vowel = ref('');

</script>

<template>
    <Head title="App" />

    <div class="flex justify-center pt-16">
        <!-- Search Area -->
        <div>
            <input
                v-model="vowel"
                id="search_text"
                type="text"
                list="suggestions"
                placeholder="Start Typing A Word..."
                class="block text-gray-800 w-96 h-16"
            >
            <datalist id="suggestions" v-if="vowels.includes(vowel)">
                <option v-for="verb in verbs" :value="vowel+verb"></option>
            </datalist>
        </div>
    </div>
</template>

