<template>
  <div class="carousel-section">
    <!-- Carousel -->
    <Carousel @slide-end="handleSlideEnd">
      <Slide v-for="(slide, index) in 4" :key="index">
        <div class="carousel__item">
          <!-- Display different messages based on the slide index -->
          <template v-if="index === 0">
            <p class = "pstyle">What is the capital of Portugal? 🇵🇹</p>
          </template>

          <template v-else-if="index === 1">
            <div class="carousel__content">
              <form @submit.prevent="submitBirthdate">
                <label for="birthdate" class = "pstyle">When were you born?</label>
                <input type="date" id="birthdate" v-model="birthdate" min="1900-01-01" max="2024-12-31" required>
                <button type="submit" :disabled="!birthdate">Submit</button> <!-- Disable the button if birthdate is not filled -->
              </form>
            </div>
          </template>

          <template v-else-if="index === 2">
            <div class="flex-container">
              <div class="box box1">Journey into the World of Pokémon</div>
              <div class="box box2">Pokémon Trainer</div>
              <div class="box box3">Workshop</div>
              <div class="box box4">by Professor Oak</div>
              <div class="box box5">Embark on an epic Pokémon adventure! Join our Trainer Workshop led by Professor Oak. 
                Learn to capture, train, and battle Pokémons as you explore diverse landscapes, meet fascinating creatures, 
                and forge friendships. Ready to become a Pokémon Master?
              </div>
            </div>
          </template>

          <template v-else-if="index === 3">
            <img src="./assets/challenge.png" alt="Web Dev Image" class="fit-image" />
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
      birthdate: null, // Initialize birthdate as null
      submittedBirthdate: null // Track submitted birthdate separately
    };
  },
  computed: {
    formattedBirthdate() {
      if (!this.submittedBirthdate) return ''; // Show nothing until submitted
      const date = new Date(this.submittedBirthdate);
      const day = (date.getDate() ).toString().padStart(2, '0');
      const month = (date.getMonth() + 1).toString().padStart(2, '0');
      const year = date.getFullYear().toString().padStart(4, 'y');
      return `${day}-${month}-${year}`;
    },
    birthdateComplete() {
      return this.submittedBirthdate !== null; // Check if birthdate is submitted
    }
  },

  
  methods: {
    handleSlideEnd(event) {
      const newIndex = event.currentSlideIndex;
      this.currentSlideIndex = newIndex;
    },
    submitBirthdate() {
      console.log("Birthday submitted!");
      this.submittedBirthdate = this.birthdate; // Update submitted birthdate
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
  font-size: 20px;
}

.flex-container {
  display: flex;
  flex-direction: column; /* Arrange items in a column */
  align-items: flex-start; /* Align items to the start of the container */
  max-width: 800px; /* Adjust as needed */
  margin: auto; /* Center horizontally */
}

.box {
   /* Add background color */
  margin-bottom: 10px; /* Add margin between boxes */
  padding: 10px 50px; /* Add padding with 20px left and right */
   /* Set font size to larger */
  text-align: left; /* Align text to the left */
}

.box1 {
  width: 100%; /* 100% width */
  height: 50px; /* Size L */
  font-size: 35px;
  
}

.box2{
  width: 50%; /* 50% width */
  height: 35px; /* Size M */
  font-size: 35px;


}

.box3{
  width: 50%; /* 50% width */
  height: 40px; /* Size M */
  font-size: 30px;


}
.box4 {
  width: 50%; /* 50% width */
  height: 35px; /* Size M */
  font-size: 20px;
}

.box5 {
  width: 100%; /* 100% width */
  height: 150px; /* Size L */
  margin-top: 20px; /* Big gap between 4th and 5th */
}
.pstyle{
  font-size: 35px;
}
.box2 {
  margin-bottom: 5px; /* Small gap between 2nd and 3rd */
}

.box3 {
  margin-bottom: 5px; /* Small gap between 3rd and 4th */
}

.carousel__content form {
  display: flex;
  flex-direction: column;
}

.carousel__content label,
.carousel__content input,
.carousel__content button {
  margin-bottom: 10px;
}


</style>
