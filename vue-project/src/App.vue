<template>
  <div class="carousel-section">
    <!-- Carousel -->
    <Carousel @slide-end="handleSlideEnd">
      <Slide v-for="(slide, index) in 4" :key="index">
        <div class="carousel__item">
          <!-- Display different messages based on the slide index -->
          <template v-if="index === 0">
            <p>What is the capital of Portugal? 🇵🇹</p>
          </template>


          <template v-else-if="index === 1">
            <div class="carousel__content">
              <form @submit.prevent="submitBirthdate">
                <label for="birthdate">When were you born?</label>
                <input type="date" id="birthdate" v-model="birthdate" max="9999-12-31" required>
                <button type="submit">Submit</button>
              </form>
            </div>
          </template>


          <template v-else-if="index === 2">
            <div class="flex-container">
              <div class="box">Journey into the World</div>
              <div class="box">of Pokémon</div>
              <div class="box">Pokémon Trainer Workshop</div>
              <div class="box">by Professor Oak</div>
              <div class="box">Embark on an epic adventure through the enchanting world of Pokémon! Join us for a Pokémon Trainer Workshop led by the esteemed Professor Oak. Learn the art of capturing, training, and battling with Pokémon as you traverse diverse landscapes, encounter fascinating creatures, and forge lifelong friendships. Are you ready to become the ultimate Pokémon Master?</div>
            </div>
          </template>


          <template v-else-if="index === 3">
            <img src="./assets/challenge.png" alt="Your Image" class="fit-image" />
          </template>
        </div>
      </Slide>

      <template #addons>
        <Navigation />
        <Pagination />
      </template>
    </Carousel>

    <!-- Message outside the carousel -->
    <template v-if="currentSlideIndex === 0">
      <p class="answer">The capital of Portugal is Lisbon.</p>
    </template>
    <template v-else-if="currentSlideIndex === 1">
      <p class="answer" v-if="birthdateComplete">You were born on: {{ formattedBirthdate }}</p>
    </template>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import { Carousel, Navigation, Pagination, Slide } from 'vue3-carousel';

import 'vue3-carousel/dist/carousel.css';

export default {
  name: 'Basic',
  components: {
    Carousel,
    Slide,
    Pagination,
    Navigation,
  },
  data() {
    return {
      currentSlideIndex: 0,
      birthdate: null,
    };
  },
  computed: {
    formattedBirthdate() {
      if (!this.birthdate) return '';
      const date = new Date(this.birthdate);
      const day = date.getDate().toString().padStart(2, '0');
      const month = (date.getMonth() + 1).toString().padStart(2, '0');
      const year = date.getFullYear().toString().padStart(4, 'x');
      return `${day}-${month}-${year}`;
    },
    birthdateComplete() {
      return this.birthdate;
    }
  },
  methods: {
    handleSlideEnd(event) {
      const newIndex = event.currentSlideIndex;
      this.currentSlideIndex = newIndex;
    },
    submitBirthdate() {
      // Handle form submission if needed
    }
  },
};
</script>

<style>
.carousel-section {
  max-width: 800px; /* Adjust as needed */
  margin: auto auto;
}

.carousel__item {
  max-height: 500px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}



.carousel__content {
  max-width: 80%; /* Adjust as needed */
}

.carousel__slide {
  padding: 10px;
}

.carousel__prev,
.carousel__next {
  box-sizing: content-box;
  border: 0px solid white;
}

.fit-image {
  max-width: 75%;
  max-height: 75%;
  object-fit: contain;
}

.answer {
  display: flex;
  justify-content: center;
  align-items: center;
}

.flex-container {
  display: flex;
  flex-direction: column; /* Arrange items in a column */
  justify-content: flex-start; /* Align items to the start of the container (top) */
  align-items: flex-start;
  max-height: 500px;
  width: 75%;
}

.box {
  width: 200px; /* Adjust width as needed */
  height: 50px; /* Adjust height as needed */
  background-color: green; /* Add background color */
  margin-bottom: 10px; /* Add margin between boxes */
}
</style>
