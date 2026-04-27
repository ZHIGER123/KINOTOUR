<template>
  <div>
    <!-- Filters Bar -->
    <div class="bg-light border-bottom py-3 mb-4">
      <div class="container">
        <div class="d-flex flex-wrap align-items-center gap-2">
          <select class="form-select form-select-sm w-auto">
            <option value="">Genre</option>
            <option>Action</option>
            <option>Drama</option>
            <option>Comedy</option>
            <option>Horror</option>
            <option>Sci-Fi</option>
          </select>

          <select class="form-select form-select-sm w-auto">
            <option value="">Country</option>
            <option>USA</option>
            <option>UK</option>
            <option>France</option>
            <option>Germany</option>
          </select>

          <div class="ms-auto d-flex flex-wrap gap-2">
            <button
              class="btn btn-sm"
              :class="sortBy === 'name' ? 'btn-dark' : 'btn-outline-secondary'"
              @click="sortBy = 'name'"
            >NAME</button>

            <button
              class="btn btn-sm"
              :class="sortBy === 'year' ? 'btn-dark' : 'btn-outline-secondary'"
              @click="sortBy = 'year'"
            >YEAR</button>

            <button
              class="btn btn-sm"
              :class="sortBy === 'rating' ? 'btn-dark' : 'btn-outline-secondary'"
              @click="sortBy = 'rating'"
            >RATING</button>

            <button class="btn btn-sm btn-outline-secondary" @click="toggleDir">
              {{ sortDir === 'asc' ? '↑' : '↓' }}
            </button>

            <button class="btn btn-sm btn-outline-danger" @click="resetFilters">
              RESET
            </button>
          </div>
        </div>
      </div>
    </div>

    
    <div class="container">
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4 mb-5">
        <div v-for="film in films" :key="film.id" class="col">
          <div class="card h-100 shadow-sm">

           
            <div
              class="bg-secondary d-flex align-items-center justify-content-center overflow-hidden"
              style="height: 200px;"
            >
              <img
                v-if="film.poster"
                :src="film.poster"
                :alt="film.title"
                class="w-100 h-100 object-fit-cover"
              />
              <svg v-else width="64" height="64" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
                <circle cx="40" cy="40" r="28" stroke="white" stroke-width="2" opacity="0.5"/>
                <polygon points="32,28 58,40 32,52" fill="white" opacity="0.5"/>
              </svg>
            </div>

           
            <div class="card-body d-flex flex-column">
              <h5 class="card-title mb-1">{{ film.title }}</h5>
              <p class="text-muted small mb-1">
                <span class="text-warning fw-bold">★</span> {{ film.rating }}
              </p>
              <p class="text-muted small mb-2">{{ film.duration }} min</p>
              <div class="d-flex flex-wrap gap-1 mb-3">
                <span
                  v-for="g in film.genres"
                  :key="g"
                  class="badge bg-secondary"
                >{{ g }}</span>
              </div>
              <div class="mt-auto">
                <NuxtLink :to="`/films/${film.id}`" class="btn btn-dark btn-sm">
                  VIEW
                </NuxtLink>
              </div>
            </div>

          </div>
        </div>
      </div>

      
      <nav class="d-flex justify-content-center mb-5">
        <ul class="pagination">
          <li
            v-for="p in totalPages"
            :key="p"
            class="page-item"
            :class="{ active: currentPage === p }"
          >
            <button class="page-link" @click="currentPage = p">{{ p }}</button>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const sortBy = ref('name')
const sortDir = ref('asc')


const films = ref([
  { id: 1, title: 'Inception',       rating: 8.8, duration: 148, year: 2010, genres: ['Sci-Fi', 'Thriller'],   poster: '' },
  { id: 2, title: 'The Godfather',   rating: 9.2, duration: 175, year: 1972, genres: ['Crime', 'Drama'],       poster: '' },
  { id: 3, title: 'Interstellar',    rating: 8.6, duration: 169, year: 2014, genres: ['Sci-Fi', 'Adventure'],  poster: '' },
  { id: 4, title: 'Parasite',        rating: 8.5, duration: 132, year: 2019, genres: ['Thriller', 'Drama'],    poster: '' },
  { id: 5, title: 'The Dark Knight', rating: 9.0, duration: 152, year: 2008, genres: ['Action', 'Crime'],      poster: '' },
  { id: 6, title: 'Pulp Fiction',    rating: 8.9, duration: 154, year: 1994, genres: ['Crime', 'Drama'],       poster: '' },
])

function toggleDir() {
  sortDir.value = sortDir.value === 'asc' ? 'desc' : 'asc'
}

function resetFilters() {
  sortBy.value = 'name'
  sortDir.value = 'asc'
  currentPage.value = 1
}
</script>