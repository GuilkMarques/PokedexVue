<template>
  <div class="pokemon">
    <div class="card"  :key="index">
      <div class="card-image">
        <figure>
          <img :src="currentImage" alt="Pokemon image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} {{ formattedName }}</p>
            <p class="subtitle is-6">{{ pokemon.type.join(', ') }}</p>
          </div>
        </div>
        <div class="content">
          <button class="button is-normal is-responsive" @click="toggleImage">
            {{ isFront ? 'Frente' : 'Costas' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  created: function () {
    axios.get(this.url).then(response => {
      this.pokemon.type = response.data.types.map(type => type.type.name);
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
      this.currentImage = this.pokemon.front;
    });
  },
  data() {
    return {
      isFront: true,
      currentImage: '',
      pokemon: {
        type: [],
        front: '',
        back: '',
      },
    };
  },
  props: {
    name: String,
    url: String,
    num: Number,
  },
  computed: {
    formattedName() {
      return this.name.replace(/\b\w/g, char => char.toUpperCase());
    },
  },
  methods: {
    toggleImage() {
      this.isFront = !this.isFront;
      this.currentImage = this.isFront ? this.pokemon.front : this.pokemon.back;
    },
  },
};
</script>

<style>
.pokemon {
  display: grid;
  grid-template-columns: auto; /* Organiza os cards em 3 colunas */
  gap: 20px; /* Espaçamento entre os cards */
  padding: 10px;
}

.card {
  width: 100%;
  max-width: 300px; /* Limita a largura dos cards */
}
</style>
