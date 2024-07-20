<script>
import axios from 'axios';
import TicketModal from '@/components/TicketModal.vue'


export default {
    components: { TicketModal },
    data() {
        return {
            movies: [],
            isModalVisible: false,
            selectedMovie: null,
        }
    },

    mounted() {
        this.fetchMovies();
    },

    methods: {
        async fetchMovies() {
            const token = 'eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI1ZjY0ZjkyMzQ3MGMyODA1OWE5OTUzYjM2ZWEzYzlmZSIsIm5iZiI6MTcxOTM2OTUxNy40NTA4MzMsInN1YiI6IjY2NmNmNDdmZjUyYzE3YTNkMjk5OTE1NiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.GEpGSY1XrpbSfIZbyBui_cffKOiIn4m8eqUPoCv4y_4'; // Ensure the token is on a single line
            
            try {
            const response = await axios.get('https://api.themoviedb.org/3/discover/movie', {
                params: {
                include_adult: false,
                include_video: false,
                language: 'en-US',
                page: 1,
                sort_by: 'popularity.desc',
                },
                headers: {
                Authorization: `Bearer ${token}`,
                },
            });
            this.movies = response.data.results;
            } catch (error) {
            console.error('Error fetching movies:', error.response ? error.response.data : error.message);
            if (error.response) {
                console.error('Error Response:', error.response);
                console.error('Error Headers:', error.response.headers);
            }
            }
        },

        showModal(movie) {
            this.selectedMovie = movie;
            this.isModalVisible = true;
        },
    },

}

</script>

<template>

    <div class="card-movie-list">
        <ul class="grid grid-cols-1 xl:grid-cols-3 gap-y-10 gap-x-6 items-start p-8">
            <li class="relative flex flex-col sm:flex-row xl:flex-col items-start" v-for="movie in movies" :key="movie.id">
                <div class="order-1 sm:ml-6 xl:ml-0">
                    <h3 class="mb-1 text-slate-900 font-semibold">
                        <span class="mb-1 block text-sm leading-6 text-indigo-500">GENRE</span>{{ movie.title }}
                        
                    </h3>
                    <!-- <h5 class="text-mute">{{ movie.release_date }}</h5> -->
                    <div class="prose prose-slate prose-sm text-slate-600">
                        <p>{{ movie.overview }}</p>
                    </div>
                    <div class="rating-voter flex center my-2">
                        <svg width="25" height="25" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2.25l2.481 5.034 5.536.805-4.007 3.906.946 5.518L12 14.875l-4.956 2.638.946-5.518-4.007-3.906 5.536-.805L12 2.25z" fill="currentColor"/>
                        </svg>
                        <span>
                            {{ movie.vote_count }}
                        </span>
                    </div>
                    <a
                        class="group inline-flex items-center h-9 rounded-full text-sm font-semibold whitespace-nowrap px-3 focus:outline-none focus:ring-2 bg-slate-100 text-slate-700 hover:bg-slate-200 hover:text-slate-900 focus:ring-slate-500 mt-6"
                        href=""  @click.prevent="showModal(movie)">Scan For Ticket<span class="sr-only"></span>
                        <svg class="overflow-visible ml-3 text-slate-300 group-hover:text-slate-400"
                            width="3" height="6" viewBox="0 0 3 6" fill="none" stroke="currentColor" stroke-width="2"
                            stroke-linecap="round" stroke-linejoin="round">
                            <path d="M0 0L3 3L0 6"></path>
                    </svg></a>
                    
                    
                </div>

                <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
                :alt="movie.title" class="mb-6 shadow-md rounded-lg bg-slate-50 w-full sm:w-[17rem] sm:mb-0 xl:mb-6 xl:w-full" width="1216" height="640">
            </li>
            
        </ul>

        <!-- Modal Component -->
        <!-- <TicketModal /> -->
        <TicketModal v-if="isModalVisible" @close="isModalVisible = false" :movie="selectedMovie"></TicketModal>
    </div>
</template>


<style scoped></style>