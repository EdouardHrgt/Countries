<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@300;600;800&display=swap');
:root {
  /* COLORS */
  --clr-white: hsl(0, 0%, 100%);
  --light-gray: hsl(0, 0%, 98%);
  --clr-dark-gray: hsl(0, 0%, 52%);
  --clr-dark-blue: hsl(209, 23%, 22%);
  --clr-darker-blue-dark-mode: hsl(207, 26%, 17%);
  --clr-darker-blue: hsl(200, 15%, 8%);
  --clr-black: black;
  --clr-shadow: #d3d3d3;
  --clr-light-bg: #f6f6f6;
  /* FONTS */
  --h1-size: 24px;
  --h2-size: 18px;
  --h2-line: 26px;
  --p-size: 14px;
  --p-line: 16px;
  --form-line: 20px;
  --form-size: 16px;

  /* SIZES */
  --pc-width: 1440px;
  --tab-width: 900px;
  --mobile-width: 350px;
}

a {
  all: unset;
}

h1,
h2,
p,
span,
a,
input[type='search'],
input[type='search']::placeholder,
option,
option:disabled,
select {
  color: var(--clr-darker-blue);
}

input[type='search'],
input[type='search']::placeholder,
select {
  background-color: var(--clr-white);
}

.dark {
  --clr-white: hsl(209, 23%, 22%); /*ok*/
  --light-gray: hsl(209, 23%, 22%);
  --clr-dark-gray: #d3d3d3;
  --clr-darker-blue: hsl(0, 0%, 100%);
  --clr-black: hsl(0, 0%, 100%); /*ok*/
  --clr-shadow: hsl(208, 22%, 14%); /*ok*/
  --clr-light-bg: hsl(207, 26%, 17%); /*ok*/
}

* {
  font-family: 'Nunito Sans', sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  list-style: none;
}

h1 {
  font-size: var(--h1-size);
  font-weight: 800;
}

h2 {
  font-size: var(--h2-size);
  line-height: var(--h2-line);
  font-weight: 800;
  margin-bottom: 1rem;
}

p {
  font-size: var(--p-size);
  line-height: var(--p-line);
}

/*GLOBAL WIDTH*/
.home-page,
.about-page {
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
  cursor: pointer;
}

.dark-mode p {
  margin-left: 0.5rem;
}
</style>
