<template>
    <div class="movie-layout" v-if="movie">
        <div class="poster">
            <img :src="movie.posterUrl" alt="Movie Poster" />
        </div>
        <div class="details">
            <h1>{{ movie.title }} <span>({{ movie.year }})</span></h1>
            <p class="info">{{ movie.released }} · {{ movie.genre }} · {{ movie.runtime }}</p>
            <div class="score">
                <span class="user-score">
                    <span class="metaScore">
                        <span class="metaScore-value">{{ movie.metaScore }} <span>%</span></span>
                    </span>
                    <p style="width: min-content;">User Score</p>
                </span>
                <span class="more">☰</span>
                <span class="heart">Heart</span>
                <span class="bookmark">Bookmark</span>
                <span class="like">Like</span>
                <span class="play-trailer">Play Trailer</span>
            </div>
            <!-- <button class="trailer-btn">Play Trailer</button> -->
            <h2>Overview</h2>
            <p>{{ movie.plot }}</p>
            <ul>
                <li><strong>Director</strong>: {{ movie.director }}</li>
                <li><strong>Writer(s)</strong>: {{ movie.writer }}</li>
                <li><strong>Actors</strong>: {{ movie.actors }}</li>

            </ul>
        </div>
    </div>
    <div v-else>
        <p>Loading movie details...</p>
    </div>
</template>

<script>
import { API_I, API_KEY, BASE_URL } from '@/utils/constants';

export default {
    data() {
        return {
            movie: null, // Holds the movie data from the API
        };
    },
    methods: {
        async fetchMovieData() {
            try {
                const response = await fetch(`${BASE_URL}/?i=${API_I}&apikey=${API_KEY}`);
                if (!response.ok) throw new Error("Failed to fetch data");
                const data = await response.json();
                this.movie = {
                    title: data.Title,
                    year: data.Year,
                    released: data.Released,
                    runtime: data.Runtime,
                    genre: data.Genre,
                    director: data.Director,
                    writer: data.Writer,
                    actors: data.Actors,
                    plot: data.Plot,
                    language: data.Language,
                    country: data.Country,
                    posterUrl: data.Poster,
                    imdbRating: data.imdbRating,
                    imdbVotes: data.imdbVotes,
                    metaScore: data.Metascore,
                };
            } catch (error) {
                console.error("Error fetching movie data:", error);
            }
        },
    },
    mounted() {
        this.fetchMovieData();
    },
};
</script>

<style scoped>
.movie-layout {
    display: flex;
    gap: 40px;
    padding: 30px;
    background-color: #032541;
    color: #fff;
}

.poster img {
    width: 300px;
    border-radius: 10px;
}

.details {
    flex: 1;
}

.details h1 {
    font-size: 2em;
}

.details .info {
    margin: 10px 0;
    color: #fff;
    font-weight: 500;
}

.score {
    display: flex;
    align-items: center;
    gap: 40px;
    margin: 10px 0;
}

.score span {
    font-size: 1.2em;
    font-weight: bold;
    color: #76c7c0;
}

.trailer-btn {
    margin: 20px 0;
    padding: 10px 20px;
    background-color: #ff9800;
    border: none;
    color: #fff;
    border-radius: 5px;
    cursor: pointer;
}

.trailer-btn:hover {
    background-color: #e68900;
}

.creators ul {
    list-style: none;
    padding: 0;
}

.creators li {
    margin: 5px 0;
}

.metaScore {
    width: 65px;
    height: 65px;
    border-radius: 50%;
    background: conic-gradient(#21d07a 76%, #0b2b4e 0);
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.2);
}

.metaScore::before {
    content: '';
    width: 55px;
    height: 55px;
    border-radius: 50%;
    background: #0b2b4e;
    position: absolute;
    z-index: 1;
}

.metaScore-value {
    position: relative;
    font-size: 1rem;
    font-weight: bold;
    color: white;
    z-index: 2;
    display: flex;
    justify-content: center;
    align-items: center;
}

.metaScore-value span {
    font-size: small;
}

.user-score {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 10px;
}

ul {
    list-style-type: none;
    line-height: 3rem;
    padding-inline-start: 0;
}

@media (max-width: 768px) {
    .movie-layout {
        flex-direction: column;
    }
    .more, .heart, .bookmark, .like {
        display: none;
    }
    .score {
        justify-content: space-between;
    }
}
</style>