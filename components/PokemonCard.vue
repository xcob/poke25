<template>
    <div class="card-grid">
    
     <div class="card-container" v-for="card in pokemonCards" :key="card.id">
         <img :src="card.images.small" />
        {{ card.name }}
     </div>
    </div>
  </template>
  
  <script>
   import pokemon from './pokemontcgsdk'
  
  export default {
    data() {
      return {
        pokemonCards: [],
      };
    },
    async mounted() {

      pokemon.configure({apiKey: 'e38d844a-8847-4f0e-a4ff-57d03d643b16'})
      pokemon.card.where({ pageSize: 10, page: 1 })
      .then(result => {
          const cardData = result.data; // Access the data after successful retrieval
          const cardNames = cardData.map(card => card); // Use map() for efficient transformation
          this.pokemonCards = cardNames;
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
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
  }

  .card-container{
    display: flex;
    flex-direction: column;    
    align-items: center;
  }
  
  .loading,
  .error {
    text-align: center;
  }
  
  /* Add custom styles for nuxt-card based on your design preferences */
  </style>