<script setup>
import {Head} from "@inertiajs/vue3";
import {ref} from "vue";

const vowel = ref('');
const vowels = ['a', 'e', 'e', 'i', 'o', 'o', 'u'];

const verbs = [
    'bà', 'bë', 'bò', 'bo', 'bó', 'bö', 'dá', 'dé', 'ga', 'gò', 'go', 'gbë', 'gbo', 'jà', 'já', 'jö', 'ké', 'lè', 'lé', 'mì', 'mò',
    'nú', 'pá', 'p', 'ra', 'so', 'sà', 'ta', 'wo', 'wò', 'ya', 'yé', 'yò'
];

const meanings = [
    'Village', 'Blade', 'Secure', 'Female', 'Half', 'Plate', 'Cutlass', 'Crown', 'Chair', 'Cage', 'Clock', 'Farmer', 'Concoction', 'Roof',
    'Dog', 'Contribution', 'Axe', 'Concubine', 'Night', 'Sign', 'Clay', 'Mercy', 'Arm', 'Pocket', 'Body', 'Cloth', 'Culture', 'Pepper', 'Plate',
    'Skin', 'Wife', 'World', 'Joy'
];
const verbMeanings = [
    {word: "bà", meaning: "bend"},
    {word: "bë", meaning: "peel"},
    {word: "bò", meaning: "cover"},
    {word: "bo", meaning: "cover"},
    {word: "bó", meaning: "cover"},
    {word: "dá", meaning: "created"},
    {word: "dé", meaning: "cover"},
    {word: "go", meaning: "lay in wait"},
    {word: "gbà", meaning: "agreed"},
    {word: "gbo", meaning: "crush leaves in water"},
    {word: "jà", meaning: "fight"},
    {word: "já", meaning: "fight"},
    {word: "jo", meaning: "resemble"},
    {word: "mì", meaning: "shake"},
    {word: "mò", meaning: "mold"},
    {word: "pá", meaning: "kill"},
    {word: "ra", meaning: "buy"},
    {word: "sa", meaning: "select"},
    {word: "wo", meaning: "see"},
    {word: "ya", meaning: "tear"},
    {word: "ye", meaning: "understand"},
];

const wordMeaning = ref('');
const verbMeaning = ref('');
const verbHasMeaning = ref(false);
const verbWithoutMeaning = ref('');
const verbWithMeaning = ref('');
const concatWord = () => {
    let data = verbMeanings.filter(e => e.word.toLowerCase() === vowel.value.substring(1, vowel.value.length));
    if (data.length > 0) {
        verbHasMeaning.value = true;
        verbWithMeaning.value = vowel.value.substring(1, vowel.value.length);
    } else {
        verbHasMeaning.value = false;
        verbWithoutMeaning.value = vowel.value.substring(1, vowel.value.length);
    }
    wordMeaning.value = meanings[verbs.indexOf(vowel.value.substring(1, vowel.value.length))];
    let temp = verbMeanings.filter(e => e.word.toLowerCase() === vowel.value.substring(1, vowel.value.length));
    verbMeaning.value = temp[0].meaning;
};

</script>

<template>
    <Head title="App" />

    <div class="min-h-screen pt-32 bg-neutral-100">
        <h1 class="text-gray-800 font-bold text-2xl text-center mb-8 uppercase tracking-wide">Morphological Tagging</h1>
        <div class="max-w-2xl mx-auto border border-gray-400 rounded p-12">
            <!-- Search Area -->
            <div>
                <input
                    v-model="vowel"
                    id="search_text"
                    type="text"
                    list="suggestions"
                    placeholder="Start Typing A Word..."
                    class="block text-gray-800 w-full h-16"
                    @change="concatWord"
                >
                <datalist id="suggestions" v-if="vowels.includes(vowel)">
                    <option v-for="verb in verbs" :value="vowel+verb"></option>
                </datalist>
            </div>

            <div class="mt-8" v-if="vowel && !verbHasMeaning">
                <p>Monosyllabic lexical item "<span class="font-bold">{{verbWithoutMeaning}}</span>" does not have a meaning</p>
            </div>
            <div class="mt-8" v-if="vowel && verbHasMeaning">
                <p>"<span class="font-bold">{{verbWithMeaning}}</span>" means {{verbMeaning}}</p>
            </div>

            <div v-if="wordMeaning" class="mt-8 flex items-center space-x-8 text-lg">
                <h2 class="text-gray-800 font-medium">Word Meaning: </h2>
                <p class="text-blue-500 font-semibold">{{wordMeaning}}</p>
            </div>
        </div>
    </div>
</template>

