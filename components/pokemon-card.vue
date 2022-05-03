<template>
  <div class="card is-shadowless is-clipped">
    <div class="card-image">
      <figure class="image pokemon-card-image is-flex is-align-items-center is-justify-content-center has-background-grey-lighter">
        <img v-bind:src="this.pokemon.imageURL" :alt="`${pokemon.name} artwork`">
      </figure>
    </div>
    <p v-if="$fetchState.pending">
      Loading Pokemon details...
    </p>
    <p v-else-if="$fetchState.error">
      Error occured when loading card.
    </p>
    <div v-else class="card-content pokemon-card-content p-6">
      <h4 class="title is-4 mb-3">{{pokemon.name}}</h4>
      <p><strong>Abilities: </strong>{{pokemon.abilities.reduce((prev, curr) => prev + ", " + curr)}}</p>
      <p><strong>Types: </strong>{{pokemon.types.reduce((prev, curr) => prev + ", " + curr)}}</p>
      <p><strong>HP: </strong>{{pokemon.stats.hp}}</p>
      <p><strong>Attack: </strong>{{pokemon.stats.attack}}</p>
      <p><strong>Defense: </strong>{{pokemon.stats.defense}}</p>
      <pokemon-detail-modal :pokemon="this.pokemon" />
    </div>
  </div>
</template>

<script>
import pokemonDetailModal from './pokemon-detail-modal.vue';
  export default {
  components: { pokemonDetailModal },
    props: {
      pokemonId: String
    },
    data () {
      return { 
        pokemon: []
      }
    },
    async fetch () {
      this.pokemon = await fetch(
        `https://pokeapi.co/api/v2/pokemon/${this.pokemonId}`
      ).then(async res => {
        let processedData = {
          name: "",
          stats: {},
          imageURL: "",
          abilities: [],
          types: [],
        };
        let rawResponse = await res.json();

        processedData.imageURL = rawResponse.sprites.other['official-artwork'].front_default;
        processedData.name = rawResponse.name
            .split("-")
            .map(elem => elem.charAt(0).toUpperCase() + elem.substring(1))
            .reduce((prev, curr) => prev + " " + curr);

        rawResponse.stats.forEach((element) => {
          processedData.stats[element.stat.name] = element.base_stat;
        });

        rawResponse.abilities.forEach((element) => {
          processedData.abilities.push(element.ability.name
            .split("-")
            .map(elem => elem.charAt(0).toUpperCase() + elem.substring(1))
            .reduce((prev, curr) => prev + " " + curr)
          );
        });

        rawResponse.types.forEach((element) => {
          processedData.types.push(element.type.name
            .split("-")
            .map(elem => elem.charAt(0).toUpperCase() + elem.substring(1))
            .reduce((prev, curr) => prev + " " + curr)
          );
        });

        return processedData;
      });
    }
  }
</script>