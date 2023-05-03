<template>
  <div class="about">
    <div class="about-page" :class="{ dark: isDark }">
      <!-- HEADER -->
      <header>
        <nav>
          <h1>Where in the world?</h1>
          <div class="dark-mode" @click="isDark = !isDark">
            <p>Dark Mode</p>
          </div>
        </nav>
      </header>
      <main>
        <router-link :to="{ path: '/' }" class="back-link">Back</router-link>
        <div class="country">
          <div class="flag">
            <img :src="country[0].flag" :alt="'flag of: ' + country[0].name" />
          </div>
          <div class="infos">
            <div class="infos-left">
              <h2>{{ country[0].name }}</h2>
              <p>
                Native Name: <span>{{ country[0].nativeName }}</span>
              </p>
              <p>
                Population: <span>{{ country[0].population }}</span>
              </p>
              <p>
                Region: <span> {{ country[0].region }}</span>
              </p>
              <p>
                Sub Region: <span> {{ country[0].subregion }}</span>
              </p>
              <p>
                Capital: <span> {{ country[0].capital }}</span>
              </p>
            </div>
            <div class="infos-right">
              <p>
                Top Level Domain: <span>{{ country[0].topLevelDomain[0] }}</span>
              </p>
              <p>
                Currencies: <span>{{ country[0].currencies[0].code }}</span>
              </p>
              <p>
                Languages: <span>{{ country[0].languages[0].name }}</span>
              </p>
            </div>
            <div class="borders">
              <p>
                Border Countries: <br />
                <span class="border" v-for="border in country[0].borders" :key="border">{{
                  border
                }}</span>
              </p>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import data from '/data.json';
export default {
  data() {
    return {
      country: null,
      isDark: false,
    };
  },
  created() {
    this.country = data.filter((n) => n.name === this.$route.params.name);
  },
};
</script>

<style scoped>
main {
  min-height: calc(100vh - 81px);
}

.back-link {
  font-weight: 800;
  letter-spacing: 1px;
  cursor: pointer;
  background-color: var(--clr-shadow);
  padding: 0.2rem 1.5rem;
  border-radius: 5px;
}

h2 {
  font-size: 32px;
  margin-bottom: 2rem;
}

.country {
  margin: 4rem auto;
  display: flex;
  gap: 5rem;
}

.flag {
  height: 401px;
  width: 560px;
  min-height: 401px;
  min-width: 560px;
  border-radius: 10px;
  overflow: hidden;
}

.flag img {
  display: block;
  object-fit: cover;
  height: 100%;
  width: 100%;
}

.infos {
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-width: 500px;
  position: relative;
}

.borders {
  position: absolute;
  bottom: 2rem;
}

.border {
  background-color: var(--clr-shadow);
  border-radius: 3px;
  padding: 0.1rem 0.7rem;
  margin: 0 0.2rem;
}

p {
  font-size: var(--p-size);
  line-height: 1.7rem;
  font-weight: 800;
}

p span {
  font-weight: 600;
  color: var(--clr-dark-gray);
  margin-left: 0.2rem;
}

@media screen and (max-width: 1300px) {
  .country {
    gap: 2rem;
  }
  .infos {
    min-width: 450px;
  }
}

@media screen and (max-width: 1110px) {
  .infos {
    min-width: 375px;
  }
}

@media screen and (max-width: 1024px) {
  .country {
    flex-direction: column;
  }

  .flag {
    height: 229px;
    width: 320px;
    min-width: 320px;
    min-height: 229px;
    margin: auto;
  }

  .infos {
    min-width: auto;
    flex-direction: column;
    align-items: flex-start;
    width: 320px;
    margin: auto;
  }
  .borders {
    position: relative;
    bottom: unset;
  }
}
</style>
