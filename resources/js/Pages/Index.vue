<script setup>
import {Head} from "@inertiajs/vue3";
import {ref} from "vue";

const vowel = ref('');
const verbs = [
    'ba', 'be', 'bo', 'da', 'de', 'ga', 'go', 'gbe', 'ja', 'jo', 'ke', 'le', 'mi', 'mo',
    'nu', 'pa', 'p', 'ra', 'so', 'sa', 'ta', 'wo', 'ya', 'ye', 'yo'
];
const vowels = ['a','e','i','o','u'];

const meanings = [
    'Village', 'Blade', 'Secure', 'Cutlass', 'Crown', 'Chair', 'Clock', 'Farmer', 'Dog', 'Contribution', 'Axe', 'Concubine', 'Sign', 'Clay', 'Mercy', 'Arm', 'Pocket',
    'Body', 'Cloth', 'Culture', 'Pepper', 'Plate', 'Wife', 'World', 'Joy'
];
const verbMeanings = [
    {word: "ba", meaning: "bend"},
    {word: "be", meaning: "peel"},
    {word: "bo", meaning: "cover"},
    {word: "da", meaning: "created"},
    {word: "de", meaning: "arrived"},
    {word: "go", meaning: "lay in wait"},
    {word: "gbe", meaning: "bend"},
    {word: "gba", meaning: "agreed"},
    {word: "gbo", meaning: "crush leaves in water"},
    {word: "ja", meaning: "fight"},
    {word: "jo", meaning: "resemble"},
    {word: "mi", meaning: "shake"},
    {word: "mo", meaning: "mold"},
    {word: "pa", meaning: "kill"},
    {word: "ra", meaning: "buy"},
    {word: "sa", meaning: "select"},
    {word: "wo", meaning: "see"},
    {word: "le", meaning: "bend"},
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
                <p>Monosyllabic verb "<span class="font-bold">{{verbWithoutMeaning}}</span>" does not have a meaning</p>
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

