<template>
  <h1>Car Configurator</h1>
  <form @submit="addSpecification">
    <div class="form-input">
      <label for="name">Name of specification</label>
      <input
        id="name"
        required
        placeholder="Enter the name of specification"
        v-model="name"
      />
    </div>
    <div class="form-input">
      <label for="engine">Engine</label>
      <select id="engine" required v-model="engine">
        <option value="V6 Engine">V6 Engine</option>
        <option value="V8 Engine">V8 Engine</option>
        <option value="V12 Engine">V12 Engine</option>
      </select>
    </div>
    <div class="form-input">
      <label for="seats">Type of seats</label>
      <select id="seats" required v-model="seats">
        <option value="Leather">Leather</option>
        <option value="Fibric">Fibric</option>
        <option value="Nylon">Nylon</option>
        <option value="Leatherette">Leatherette</option>
      </select>
    </div>
    <div class="form-input">
      <label for="color">Color</label>
      <select id="color" required v-model="color">
        <option value="White">White</option>
        <option value="Black">Black</option>
        <option value="Blue">Blue</option>
        <option value="Red">Red</option>
        <option value="Grey">Grey</option>
      </select>
    </div>
    <div class="form-input">
      <label for="tireSize">Tire size</label>
      <select id="tireSize" required v-model="tireSize">
        <option value="19 inch">19 inch</option>
        <option value="20 inch">20 inch</option>
        <option value="21 inch">21 inch</option>
      </select>
    </div>
    <div :key="option" v-for="option in options">
      <div class="form-input">
        <label :for="option">{{ option }}</label>
        <input :id="option" required placeholder="" />
      </div>
    </div>
    <div class="button__box">
      <button @click="addOption" type="button" style="width: 250px">
        + New configuration option
      </button>
      <button type="submit">Save</button>
    </div>
  </form>
  <div :key="s.name" v-for="s in data" class="car__specification">
    <Specification :data="s" />
  </div>
  <div class="car__button-box">
    <button @click="reset" class="car__button" style="width: 250px">
      + Make new specification
    </button>
  </div>
</template>

<script>
import Specification from "./components/Specification.vue";
export default {
  name: "App",
  components: {
    Specification,
  },
  data() {
    return {
      name: "",
      engine: "V6 Engine",
      seats: "Leather",
      color: "White",
      tireSize: "19 inch",
      data: [],
      options: [],
    };
  },
  methods: {
    addSpecification(event) {
      event.preventDefault();
      let newData = [];

      this.options?.map((option) =>
        newData.push(document.getElementById(option).value)
      );
      console.log(newData);
      this.data = [
        {
          name: this.name,
          engine: this.engine,
          seats: this.seats,
          color: this.color,
          tireSize: this.tireSize,
          options: this.options,
          newData: newData,
        },
        ...this.data,
      ];
      console.log(this.data);
    },
    reset() {
      document.body.scrollTop = 0; // For Safari
      document.documentElement.scrollTop = 0; // For Chrome, Firefox, IE and Opera
      this.name = "";
      this.engine = "V6 Engine";
      this.seats = "Leather";
      this.color = "White";
      this.tireSize = "19 inch";
      this.options?.map(
        (option) => (document.getElementById(option).value = "")
      );
    },
    addOption() {
      const option = prompt("Add a new configuration option");
      this.options = [...this.options, option];
      console.log(this.options);
    },
  },
  created() {
    this.data = [
      {
        name: "Sports",
        engine: "V12 Engine",
        seats: "Leather",
        color: "Blue",
        tireSize: "20 inch",
      },
    ];
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap");
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

html {
  scroll-behavior: smooth;
}

#app {
  font-family: "Poppins", sans-serif;
  text-align: center;
  color: #2c3e50;
  padding: 40px 0;
  display: flex;
  flex-direction: column;
  width: 600px;
  margin: 0 auto;
}
button {
  outline: none;
  border: 1px solid #eee;
  width: 150px;
  height: 55px;
  font-size: 15px;
  font-weight: 400;
  text-align: center;
  border-radius: 5px;
  background-color: transparent;
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
  cursor: pointer;
  margin-left: auto;
  transition: all 0.3s ease-in-out;
  &:hover {
    background: #2c3e50;
    color: white;
    box-shadow: none;
  }
}
form {
  margin-top: 36px;
  display: flex;
  flex-direction: column;
  gap: 24px;
  width: 600px;
  margin: 36px auto 0 auto;
}
.form-input {
  display: flex;
  flex-direction: column;
  align-content: flex-start;
  gap: 8px;
  label {
    font-size: 15px;
    font-weight: 400;
    text-align: start;
  }
  input,
  select {
    padding: 16px;
    outline: none;
    border: 1px solid #eee;
    box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
    border-radius: 5px;
    font-size: 15px;
    font-weight: 400;
    text-align: start;
  }
  select {
    appearance: none;
    background-image: url("./assets/arrow.svg");
    background-repeat: no-repeat;
    background-position: calc(100% - 24px) 50%;
  }
}
.car__specification {
  display: flex;
  flex-direction: column;
  gap: 36px;
  width: 600px;
  margin: 50px auto 0 auto;
}

.car__button {
  margin: 0;
  &-box {
    margin-top: 36px;
    display: flex;
    align-content: center;
    justify-content: end;
  }
}
.button__box {
  display: flex;
  align-content: center;
  justify-content: space-between;
  button {
    margin: 0;
  }
}
</style>
