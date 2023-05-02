<template>
  <div class="home">
    <div class="home-page">
      <!-- HEADER -->
      <header>
        <nav>
          <h1>Where in the world?</h1>
          <div class="dark-mode">
            <svg xmlns="http://www.w3.org/2000/svg" width="26" height="26">
              <path
                fill-rule="evenodd"
                d="M13 0c.81 0 1.603.074 2.373.216C10.593 1.199 7 5.43 7 10.5 7 16.299 11.701 21 17.5 21c2.996 0 5.7-1.255 7.613-3.268C23.22 22.572 18.51 26 13 26 5.82 26 0 20.18 0 13S5.82 0 13 0z"
              />
            </svg>

            <p>Dark Mode</p>
          </div>
        </nav>
      </header>
      <!-- MAIN -->
      <main>
        <!-- SEARCH BAR -->
        <form>
          <div class="form-group">
            <label for="search-country" hidden>Search for a country...</label>
            <input
              type="text"
              placeholder="Search for a country"
              name="search-country"
              id="search-country"
              v-model="searchedCountry"
            />
          </div>
          <div class="form-group">
            <label for="search-region" hidden>Search by Region</label>
            <select name="search-region" id="search-region" v-model="searchedRegion">
              <option value="" disabled selected>Search by Region</option>
              <option :value="o" v-for="o in selectRegion" :key="o">{{ o }}</option>
            </select>
          </div>
        </form>
        <!-- COUNTRIES GRID -->
        <section class="grid">
          <router-link
            class="country"
            v-for="c in filterCountries"
            :key="c.name"
            :to="{ path: 'country/' + c.name }"
          >
            <div class="country-flag">
              <img :src="c.flags.svg" :alt="'flag of' + c.name" />
            </div>
            <div class="country-infos">
              <h2>{{ c.name }}</h2>
              <p class="population">
                Population: <span>{{ formatNb(c.population) }}</span>
              </p>
              <p class="region">
                Region: <span>{{ c.region }}</span>
              </p>
              <p class="capital">
                Capital: <span>{{ c.capital }}</span>
              </p>
            </div>
          </router-link>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
import data from '/data.json';
export default {
  name: 'HomeView',
  data() {
    return {
      searchedCountry: '',
      searchedRegion: '',
      countries: data,
      selectRegion: [],
    };
  },
  created() {
    const regions = this.countries.map((country) => country.region);
    this.selectRegion = [...new Set(regions)];
  },
  methods: {
    formatNb(nb) {
      return nb.toLocaleString();
    },
  },
  computed: {
    filterCountries() {
      const country = this.searchedCountry.toLowerCase();
      const region = this.searchedRegion;
      let array = this.countries;
      if (region.length) {
        array = this.countries.filter((country) => country.region == this.region);
      }
      if (country.length) {
        //
      }
      return array;
    },
  },
};
</script>

<style scoped>
/*GLOBAL WIDTH*/
.home-page {
  margin: auto;
  background-color: var(--clr-light-bg);
  padding: 0 5vw;
}

header,
form {
  margin-bottom: 3.5rem;
}

nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.48rem 0;
  box-shadow: 0 2px var(--clr-shadow);
}

.dark-mode {
  display: flex;
  align-items: center;
}

.dark-mode p {
  margin-left: 0.5rem;
}

main {
  min-height: calc(100vh - 81px);
}

form {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.form-group:nth-child(2) {
  text-align: end;
}

.form-group {
  width: 40%;
}

input[type='text'] {
  border: none;
  outline: none;
  box-shadow: 0px 2px 5px 1px var(--clr-shadow);
  font-size: var(--p-size);
  color: var(--clr-dark-gray);
  padding: 1rem;
  width: 100%;
}

input[type='text']::placeholder {
  font-size: var(--p-size);
  color: var(--clr-dark-gray);
}

select {
  padding: 1rem;
  width: 200px;
  box-shadow: 0px 2px 5px 1px var(--clr-shadow);
  border: none;
}

/*COUNTRIES GRID */
.grid {
  margin-top: 3rem;
  min-height: 50vh;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(auto, 1fr);
  grid-column-gap: 0rem;
  grid-row-gap: 4rem;
  justify-items: center;
}

.country {
  width: 264px;
  background-color: var(--clr-white);
  box-shadow: 0px 0px 12px 2px var(--clr-shadow);
  cursor: pointer;
  transition: 0.3s;
}

.country:hover {
  filter: grayscale(70%);
}

.country-flag {
  width: 100%;
  height: 160px;
}

.country-flag img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.country-infos {
  padding: 1rem;
}

.country-infos p {
  color: var(--black);
  font-weight: 600;
  margin: 0.5rem 0;
}

.country-infos span {
  font-size: var(--p-size);
  line-height: var(--p-line);
  color: var(--clr-dark-gray);
}

@media screen and (max-width: 1440px) {
}

@media screen and (max-width: 800px) {
  form {
    flex-direction: column;
    align-items: flex-start;
  }
  .form-group {
    width: 100%;
  }
  .form-group:nth-child(2) {
    text-align: start;
    margin-top: 2rem;
  }
}
</style>
