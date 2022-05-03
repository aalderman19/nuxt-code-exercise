<template>
  <div class="mt-4">
    <b-button type="button has-text-weight-semibold is-pokemon-font-size is-primary" rounded outlined @click="isModalOpen = true">Learn More</b-button>
    <b-modal v-model="isModalOpen">
      <div class="card is-flex is-flex-direction-column is-align-items-center">
        <figure class="image is-128x128 m-5">
          <img v-bind:src="this.pokemon.imageURL" :alt="`${pokemon.name} artwork`">
        </figure>
        <div class="card-content is-flex is-flex-direction-column">
          <h4 class="title is-4 mb-3">{{pokemon.name}}</h4>
          <p class="heading mb-3">{{pokemon.types.reduce((prev, curr) => prev + ", " + curr)}}</p>
          <b-tabs v-model="activeTab">
            <b-tab-item label="Stats">
              <p><strong>HP: </strong>{{pokemon.stats.hp}}</p>
              <p><strong>Attack: </strong>{{pokemon.stats.attack}}</p>
              <p><strong>Defense: </strong>{{pokemon.stats.defense}}</p>
              <p><strong>Special Attack: </strong>{{pokemon.stats['special-attack']}}</p>
              <p><strong>Special Defense: </strong>{{pokemon.stats['special-defense']}}</p>
              <p><strong>Speed: </strong>{{pokemon.stats.speed}}</p>
            </b-tab-item>
            <b-tab-item label="Abilities">
              <p>{{pokemon.abilities.reduce((prev, curr) => prev + ", " + curr)}}</p>
            </b-tab-item>
          </b-tabs>
        </div>
      </div>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    pokemon: Object
  },
  data() {
    return {
      isModalOpen: false,
      activeTab: 0,
    };
  }
}
</script>
