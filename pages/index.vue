<template>
  <NuxtLayout name="base">
    <section class="bg-gradient-to-r from-emerald-800 via-teal-200 to-sky-200 h-screen flex flex-col items-center justify-center">
        <div class="container mx-auto max-w-7xl px-4 sm:p-6 lg:px-8 flex flex-col md:flex-row items-center justify-between"> 
            <div class="text-white text-center md:text-left md:w-1/2">
                <h1 class="text-3xl md:text-5xl font-bold mb-4 animate-fade-in-down">Welcome to the Ultimate Pokemon Experience</h1>
                <p class="text-lg md:text-xl mb-6 animate-fade-in-down delay-100">Collect and Discover with our Interactive Pokedex and Exciting Card Pack Opener.</p>
            <NuxtLink class="bg-sky-100 text-emerald-800 hover:bg-emerald-700 hover:text-white px-6 py-3 mr-4 rounded-full transition duration-150 ease-in-out animate-fade-in-down delay-200" to="/dex">Explore The Dex</NuxtLink>
            <NuxtLink class="bg-emerald-700 hover:bg-sky-100 text-white hover:text-emerald-800 px-6 py-3 rounded-full transition duration-150 ease-in-out animate-fade-in-down delay-200" to="/card">Open a Pack!</NuxtLink>
            </div>
            <div class="w-100 flex justify-center items-center">
                <img src="/img/pokestop-main-opt.png" alt="Pokedex and Card Pack Opener Illustration" class="rounded-lg w-100"> 
            </div>
        </div>
    </section>

    <section class="bg-gray-100 py-16">
        <div class="container mx-auto text-center">
            <h2 class="text-2xl md:text-3xl font-semibold mb-4">Get Started Today</h2>
            <p class="text-lg md:text-xl mb-8">Embark on an unforgettable Pokemon adventure.</p>
            <NuxtLink class="bg-emerald-700 hover:bg-sky-100 text-white hover:text-emerald-800 px-6 py-3 rounded-full transition duration-150 ease-in-out" to="/card">Open a Pack!</NuxtLink>
        </div>
    </section>

    <section class="py-16">
        <div class="container mx-auto p-4 sm:p-6">
            <h2 class="text-2xl md:text-3xl font-semibold text-center mb-8">Features</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-8">
                <div class="p-4 md:p-6 bg-white rounded-lg shadow-md">
                    <h3 class="text-xl md:text-xl font-semibold mb-2">Comprehensive Pokedex</h3>
                    <p class="text-sm md:text-base">Explore the world of Pokemon with our detailed Pokedex featuring all your favorite creatures. Discover their types, stats, and learn about their unique abilities.</p>
                </div>
                <div class="p-4 md:p-6 bg-white rounded-lg shadow-md">
                    <h3 class="text-xl md:text-xl font-semibold mb-2">Thrilling Card Pack Openings</h3>
                    <p class="text-sm md:text-base">Experience the excitement of opening real or virtual Pokemon card packs. Uncover rare and powerful cards to add to your collection.</p>
                </div>
                <div class="p-4 md:p-6 bg-white rounded-lg shadow-md">
                    <h3 class="text-xl md:text-xl font-semibold mb-2">Cards from All Series</h3>
                    <p class="text-sm md:text-base">Collect cards from every Pokemon series, including classic sets and the latest releases. Build your dream deck and prepare for epic battles.</p>
                </div>
            </div>
        </div>
    </section>

  </NuxtLayout>
</template>

<script >
definePageMeta({
  layout: "base",
});
</script>

<style>
 .framed {
    border-width: 21px;
    border-style: solid;
    padding: 1em;
    margin: 1em 0 0;
    width: 100%;
    max-width: 100%;
 }
</style>
