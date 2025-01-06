<template>
    <div class="pokemon-wrapper">
      <div class="pokemon-grid">
          <div class="pokemon-card" v-for="pokemon in pokemons" :key="pokemon.name" @click="isHidden = !isHidden">
            <div class="pokemon-image-wrapper" >
              <img class="pokemon-image" :src="pokemon.image" alt="Pokémon Image"  v-show="!isHidden">
            </div>
            <div class="pokemon-info-wrapper" v-show="isHidden">
              <div class="flex flex-col md:flex-row bg-white rounded-lg shadow-md overflow-hidden" >
                <div class="md:w-1/2"> 
                  <img :src="pokemon.image"  alt="Image of Pokémon" class="w-full h-full object-cover">
                </div>
                <div class="md:w-1/2 p-6 pokemon-info">
                  <h2 class="text-xl font-semibold mb-2"> {{ pokemon.name }}</h2>
                  <p class="text-gray-700">
                    #{{ pokemon.pid }}
                  <img :src="pokemon.type" />
                    Weight: {{ pokemon.weight }}
                  </p>
                </div>
              </div>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
                <div class="p-4 bg-white rounded-lg shadow-md">
                  <ul class="list-none list-inside">
                    <li>{{ pokemon.moveOne }}</li>
                    <li>{{ pokemon.moveTwo }}</li>
                  </ul>
                </div>
                <div class="p-4 bg-white rounded-lg shadow-md">
                  <ul class="list-none list-inside">
                    <li>{{ pokemon.moveThree }}</li>
                    <li>{{ pokemon.moveFour }}</li>
                  </ul>
                </div>
              </div>
            </div>

          </div>
          
      </div>
    </div>
      
    </template>
    
   
  <script>
  
  export default {
    data() {
      return {
        pokemons: [],
        isHidden: true,
      };
    },
    async mounted() {
      const limit = 9;
      const url = `https://pokeapi.co/api/v2/pokemon/?limit=${limit}`;
  
      try {
        const response = await fetch(url);
        const data = await response.json();
        const rand1 = Math.floor(Math.random() * 30) + 1;

  
        // Loop through each Pokémon and fetch its image
        const promises = data.results.map(async (pokemon) => {
          const pokemonUrl = `https://pokeapi.co/api/v2/pokemon/${pokemon.name}`;
          const pokemonResponse = await fetch(pokemonUrl);
          const pokemonData = await pokemonResponse.json();
  
          const typeURL = pokemonData.types[0].type.url;
          const typeURLResponse = await fetch(typeURL);
          const typeURLData = await typeURLResponse.json();
          
          //console.log(pokemonData.moves);
          return {
            name: pokemonData.name,
            type: typeURLData.sprites["generation-viii"]["sword-shield"].name_icon,
           // type2: pokemonData.types[1].type.name,
            pid: pokemonData.id,
            image: pokemonData.sprites.front_default,
            weight: pokemonData.weight,
            moveOne: pokemonData.moves[rand1+1].move.name,
            moveTwo: pokemonData.moves[rand1+3].move.name,
            moveThree: pokemonData.moves[rand1+5].move.name,
            moveFour: pokemonData.moves[rand1+9].move.name
          };
        });
  
        // Wait for all image fetches to complete
        const pokemonsWithImages = await Promise.all(promises);
        this.pokemons = pokemonsWithImages;
      } catch (error) {
        console.error('Error fetching Pokémon:', error);
      }
    },
  };
  </script>
    
    <style scoped>
  
        .pokemon-wrapper{
          padding: 10px;
        }
        .pokemon-grid {
          display: grid;
          grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
          gap: 20px;
        }
  
        .pokemon-card {
          border: 1px solid #ccc;
          border-radius: 10px;
          overflow: hidden;
          padding: 20px;
          background-color: #e3e3e3;
        }
  
        .pokemon-image-wrapper{
          background-color: #fff;
          border-radius: 10px;
        }
  
        .pokemon-image {
          width: 100%;
          height: auto;
          object-fit: contain;
        }
  
        .pokemon-info {
          display: flex;
          flex-direction: column;
          text-align: center;
          text-transform: capitalize;
          font-family: 'Arial';
          font-weight: 600;
          align-items: center;
        }
    </style>