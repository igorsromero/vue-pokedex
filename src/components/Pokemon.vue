<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }}. {{ name | upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>

        <div class="content"></div>
        <button class="button is-fullwidth" id="btn-color-ig" @click="mudarSprite">
          Mudar Imagem
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
    axios
      .get(this.url)
      .then((res) => {
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.currentImg = this.pokemon.front;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods: {
    mudarSprite: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
          this.isFront = true;
          this.currentImg = this.pokemon.front;
      }
    },
  },
};
</script>

<style scoped>
#pokemon {
  margin-top: 2%;
}

#btn-color-ig {
  color: darkslategrey;
  font-weight: bold;
}
</style>