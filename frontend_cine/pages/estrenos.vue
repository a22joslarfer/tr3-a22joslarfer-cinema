<template>
    <div class="container">
        <NavBar />
        <Nuxt />


        <div class="div-movies-cont">
            <div class="div-movie-cont" v-for="estreno in  estrenos " :key="estreno.id"
                @click="navigate_to_session(estreno.id)">

                <h2 class="title">{{ estreno.title }}</h2>
                <img :src="`${estreno.poster}`" alt="" class="poster">
                <div class="div-summary-date-genre-cont">
                    <p class="synopsis">{{ estreno.synopsis }}</p>
                    <p class="date">{{ estreno.showing_date }}</p>

                    <p class="year">{{ estreno.year }}</p>
                    <p class="rating">{{ estreno.rating }}</p>
                </div>

            </div>


        </div>


        <Footer />
        <Nuxt />

    </div>
</template>



<style scoped>
/* CSS GLOBAL */
* {
    box-sizing: border-box;
    font-family: "Roboto", sans-serif;
    margin: 0;
    padding: 0px;

}


.container {
    height: auto;
    background-color: #d1d8d2;
    display: grid;
    grid-template-rows: auto auto;
    grid-template-areas:
        "nav"
        "div-movies-cont"
    ;

}

.div-movies-cont {
    display: grid;
    grid-template-rows: auto;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 20px;

}

.div-movie-cont {
    margin: 5px;
    padding: 20px;
    display: grid;
    height: 900px;
    color: #eeeeee;
    text-align: center;
    position: relative;
    border-radius: 10px;
    max-width: 600px;
    grid-template-rows: auto;
    background-color: black;
    grid-gap: 20px;
    position: relative;
    cursor: pointer;
    transition: transform 0.3s ease;

}

.div-summary-date-genre-cont {
    opacity: 0;
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.836);
    transform: translateY(-100%);
    transition: opacity 0.3s ease, transform 0.3s ease;

}

.div-movie-cont:hover .div-summary-date-genre-cont {
    opacity: 1;
    transform: translateY(0px);
    border-radius: 12px;
    height: 400px;
}


.title {
    font-size: 3em;

}

.year,
.rating,
.synopsis,
.date,
.genreId {
    font-size: 1.5em;
    margin-top: 20px;
    color: #eeeeee;
}



.poster {
    width: 100%;
    max-height: 780px;
    border-radius: 8px;
}

.synopsis {

    margin: 50px;

    font-variant: small-caps;
}
</style>

<script>
export default {
    data() {
        return {
            estrenos: []
        }
    },
    methods: {
        fetchData() {
            fetch('http://localhost:8000/api/estrenos')
                .then(response => response.json())
                .then(data => {
                    if (data) {
                        this.estrenos = data;
                        console.log('Estrenos', this.estrenos);
                        console.log('Data', data);
                    } else {
                        console.log('ERROR FETCHING DATA');
                    }
                })
                .catch(error => {
                    console.error(error);
                });
        },
        navigate_to_session(id) {
            console.log('yendo a la sesión', id)
            navigateTo(`/${id}`);

        },
    },
    mounted() {
        this.fetchData();
    },

}

</script>