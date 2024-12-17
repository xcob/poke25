<template>
  <div class="pokemon-wrapper">
    <div class="pokemon-grid">
        <div class="pokemon-card" v-for="pokemon in pokemons" :key="pokemon.name">
          <img class="pokemon-image" :src="pokemon.image" alt="Pokémon Image">
          <div class="pokemon-info">
            <h2>
              {{ pokemon.name }}
            </h2> 
            <p>
              (#{{ pokemon.pid }})
            </p>
            <p>
              {{ pokemon.type }}
            </p>
            <p>
              {{ pokemon.weight }}
            </p>
            
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
    };
  },
  async mounted() {
    const limit = 151;
    const url = `https://pokeapi.co/api/v2/pokemon/?limit=${limit}`;

    try {
      const response = await fetch(url);
      const data = await response.json();

      // Loop through each Pokémon and fetch its image
      const promises = data.results.map(async (pokemon) => {
        const pokemonUrl = `https://pokeapi.co/api/v2/pokemon/${pokemon.name}`;
        const pokemonResponse = await fetch(pokemonUrl);
        const pokemonData = await pokemonResponse.json();
        console.log(pokemonData);
        return {
          name: pokemonData.name,
          type: pokemonData.types[0].type.name,
         // type2: pokemonData.types[1].type.name,
          pid: pokemonData.id,
          image: pokemonData.sprites.front_default,
          weight: pokemonData.weight
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

      .pokemon-image {
        width: 100%;
        height: auto;
        object-fit: contain;
      }

      .pokemon-info {
        text-align: center;
        text-transform: capitalize;
        font-family: 'Arial';
        font-weight: 600;
      }
  </style>