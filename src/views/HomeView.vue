<template>
  <div class="home">
    <div class="home-page" :class="{ dark: isDark }">
      <!-- HEADER -->
      <header>
        <nav>
          <h1>Where in the world?</h1>
          <div class="dark-mode" @click="isDark = !isDark">
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
              type="search"
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
      isDark: false,
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
      if (this.searchedRegion.length) {
        return this.countries.filter((country) => country.region == this.searchedRegion);
      }
      if (this.searchedCountry.length) {
        return this.countries.filter(
          (country) => country.name.toLowerCase() == this.searchedCountry.toLowerCase()
        );
      } else {
        return this.countries;
      }
    },
  },
};
</script>

<style scoped>
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

input[type='search'] {
  border: none;
  outline: none;
  box-shadow: 0px 2px 5px 1px var(--clr-shadow);
  font-size: var(--p-size);
  padding: 1rem;
  width: 100%;
}

input[type='search']::placeholder {
  font-size: var(--p-size);
  font-weight: 600;
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
  max-height: 350px;
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
  padding: 2rem 1rem;
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

@media screen and (max-width: 1300px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media screen and (max-width: 1024px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
    width: 80%;
    margin: auto;
  }
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
  .grid {
    grid-template-columns: repeat(2, 1fr);
    width: 100%;
  }
}
@media screen and (max-width: 650px) {
  .grid {
    grid-template-columns: repeat(1, 1fr);
    grid-row-gap: 2rem;
  }
}
</style>
