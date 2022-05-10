<template>
  <form @submit.prevent="submitForm">
    <div class="form-control" :class="{ invalid: userNameInvalid }">
      <label for="user-name">Your Name</label>
      <input
        id="user-name"
        name="user-name"
        type="text"
        v-model.trim="userName"
        @blur="validateUserName"
      />
    </div>
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input
        id="age"
        name="age"
        type="number"
        v-model="userAge"
        ref="ageInput"
      />
    </div>
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select id="referrer" name="referrer" v-model="referrer">
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input
          id="interest-news"
          name="interest"
          type="checkbox"
          v-model="interest"
          value="news"
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
          id="interest-tutorials"
          name="interest"
          type="checkbox"
          v-model="interest"
          value="tutorials"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
          id="interest-nothing"
          name="interest"
          type="checkbox"
          v-model="interest"
          value="nothing"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input
          id="how-video"
          name="how"
          type="radio"
          v-model="how"
          value="video"
        />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input
          id="how-blogs"
          name="how"
          type="radio"
          v-model="how"
          value="blogs"
        />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input
          id="how-other"
          name="how"
          type="radio"
          v-model="how"
          value="other"
        />
        <label for="how-other">Other</label>
      </div>
    </div>
    <div class="form-control">
      <RatingControl v-model="rating" />
    </div>
    <div class="form-control">
      <input
        type="checkbox"
        name="confirmTerms"
        id="confirmTerms"
        v-model="agreeTerms"
      />
      <label for="confirmTerms">Agree terms of use</label>
    </div>
    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>

<script>
import RatingControl from './RatingControl.vue';
export default {
  components: {
    RatingControl,
  },
  data() {
    return {
      userName: '',
      userAge: null,
      referrer: 'wom',
      interest: [],
      how: null,
      agreeTerms: false,
      userNameInvalid: false,
      rating: null,
    };
  },
  methods: {
    submitForm() {
      console.log('User Name:', this.userName);
      console.log(typeof this.userAge); // number
      console.log(typeof this.$refs.ageInput.value); // string
      console.log(this.referrer); // logs the value of selected option
      console.log('interests checkbox:', this.interest);
      console.log('how to learn', this.how);
      console.log(this.agreeTerms);
      console.log(this.rating);
      this.userName = '';
      this.userAge = null;
      this.referrer = 'wom';
      this.interest = [];
      this.how = null;
      this.agreeTerms = false;
      this.rating = null;
    },
    validateUserName() {
      // if (this.userName) {
      //   this.userNameValidity = 'valid';
      // } else {
      //   this.userNameValidity = 'invalid';
      // }
      if (this.userName) {
        this.userNameInvalid = false;
      } else {
        this.userNameInvalid = true;
      }
    },
  },
};
</script>

<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

label {
  font-weight: bold;
}
.invalid label {
  color: red;
}
.invalid input {
  border-color: red;
}
h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>
