<template>
  <div class="container">
    <section class="section">
      <p class="heading pokemon-heading">Pokemon Cards</p>
      <h1 class="title is-size-1-desktop is-size-3-tablet is-size-3-mobile">Gotta catch ‘em all</h1>
      <div class="columns is-variable is-5-tablet is-5-desktop">
        <div class="column">
          <pokemon-card pokemonId="4" />
        </div>
        <div class="column">
          <pokemon-card pokemonId="1" />
        </div>
        <div class="column">
          <pokemon-card pokemonId="7" />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {}
</script>
