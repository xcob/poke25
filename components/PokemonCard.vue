<template>
  <div class="container mx-auto text-center">
    <div class="container " v-if="!hasLoaded">
      <div class="flex items-center justify-center h-64 w-full bg-gray-100 rounded-lg">
        <div class="w-16 h-16  rounded-full bg-emerald-800 animate-spin p-8 ">
          <div class="w-8 h-8 my-8 items-center text-center rounded-full bg-white "></div>
        </div>
      </div>
    </div>
    <div class="card-grid" v-else="hasLoaded">   
     <div class="card-container" v-for="card in pokemonCards" :key="card.id"  >
        <img :src="card.images.large" />
        <p class="card_name">{{ card.name }}</p>
        <p>Set:
           <img :src="card.set.images.logo" class="set_img" />
        </p>
        <p>{{ card.number }} / {{ card.set.total }}</p>
     </div>
    </div>
  </div>
  </template>
  
<script>
  import pokemon from 'pokemontcgsdk';
  
export default {
    data() {
      return {
        pokemonCards: [],
        hasLoaded: false,
      };
    },
    async mounted() {
      const rand1 = Math.floor(Math.random() * 30) + 1;
      pokemon.configure({apiKey: 'e38d844a-8847-4f0e-a4ff-57d03d643b16'})
      //pokemon.card.all({ q: 'set.name:Base', page=1, pageSize=250 })
      pokemon.card.where({ pageSize: 10, page: rand1 })
      .then(result => {
          const cardData = result.data; // Access the data after successful retrieval
          const cardNames = cardData.map(card => card); // Use map() for efficient transformation
          this.pokemonCards = cardNames;
          this.hasLoaded = true;
        })
        .catch(error => {
          console.error("Error fetching cards:", error); // Handle potential errors
        });
    }
}

  </script>
  
  <style scoped>
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 1rem;
  }

  .card-container{
    display: flex;
    flex-direction: column;    
    align-items: center;
  }

  .card-container .card_name{
    margin-top: 10px;
    font-size: 20px;
    font-weight: 600;
  }

  .card-container img{
    width: 325px;
    height: auto;
    border-radius: 3px;
  }

  .card-container .set_img{
    width: 80px;
    height: auto;
    margin: 10px 0px;
  }
  
  .loading,
  .error {
    text-align: center;
  }
  
  </style>