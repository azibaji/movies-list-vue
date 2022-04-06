<template>
    <div class="container">
        <div class="header">
            <router-link to="/">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M447.1 256C447.1 273.7 433.7 288 416 288H109.3l105.4 105.4c12.5 12.5 12.5 32.75 0 45.25C208.4 444.9 200.2 448 192 448s-16.38-3.125-22.62-9.375l-160-160c-12.5-12.5-12.5-32.75 0-45.25l160-160c12.5-12.5 32.75-12.5 45.25 0s12.5 32.75 0 45.25L109.3 224H416C433.7 224 447.1 238.3 447.1 256z"/></svg>
                Back
            </router-link> 
            <div>
                <p class="title">{{movieDetail.original_title}}</p>
                <p class="tag">{{movieDetail.tagline}}</p>
            </div>
        </div>
        <div class="movie-detail ">
            <div class="col-12 d-flex">
                <div class="col-4 movie-detail__img">
                    <div v-bind:style="{ backgroundImage: 'url(' + imgUrl + movieDetail.poster_path + ')' }"></div>
                </div>
                <div class="col-8 movie-detail__detail">
                    <div class="item">
                        <p class="item__title">Budget</p>
                        <p class="item__desc">
                            ${{formatPrice(movieDetail.budget)}}
                        </p>
                    </div>
                    <div class="item">
                        <p class="item__title">Revenue</p>
                        <p class="item__desc">
                            ${{formatPrice(movieDetail.revenue)}}
                        </p>
                    </div>
                    <div class="item">
                        <p class="item__title">Release date</p>
                        <p class="item__desc">
                            {{movieDetail.release_date}}
                        </p>
                    </div>
                    <div class="item">
                        <p class="item__title">Runtime</p>
                        <p class="item__desc">
                            {{formatTime(movieDetail.runtime)}}
                        </p>
                    </div>
                    <div class="item">
                        <p class="item__title">Score</p>
                        <p class="item__desc">
                            {{movieDetail.vote_average}} ({{movieDetail.vote_count}} votes)
                        </p>
                    </div>
                    <div class="item">
                        <p class="item__title">Genres</p>
                        <p class="item__desc" >
                            <span v-for="(genre, i) in movieDetail.genres" :key="genre.id">
                                {{genre.name}}
                                {{i !== movieDetail.genres.length-1 ? ', ': ''}}
                            </span>
                        </p>
                    </div>
                    <div class="item">
                        <p class="item__title">IMDB Link</p>
                        <p class="item__desc" >
                            <a :href="imdbLink+ movieDetail.imdb_id">Link</a>
                        </p>
                    </div>
                    <div class="item">
                        <p class="item__title">Home page Link</p>
                        <p class="item__desc" >
                            <a :href="movieDetail.homepage">Link</a>
                        </p>
                    </div>
                </div>
            </div>
            <div class="col-12 movie-detail__overview">
                {{movieDetail.overview}}
            </div>
            <div class="col-12 movie-detail__credit">
                <p class="title">Credit:</p>
                <p>Lorem ipsum</p>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data(){
        return{
            id: this.$route.params.id,
            movieDetail:{},
            imgUrl:'https://image.tmdb.org/t/p/w500',
            imdbLink:'https://www.imdb.com/title/'
        }
        
    },
    created(){
        this.getMovieDetail()
    },
    methods:{
        getMovieDetail(){
            axios.get(`https://api.themoviedb.org/3/movie/${this.id}?api_key=f62f750b70a8ef11dad44670cfb6aa57&language=en-US`)
            .then((response) =>{
                   this.movieDetail = response.data
                   console.log(this.movieDetail)
                })
            
        },
        formatPrice(value) {
            if(value === 0 ) return 0
            else{
                let val = (value/1).toFixed(3).replace('.', '\'')
                return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, "'")
            }
            
        },
        formatTime(value){
            let hour = Math.floor(value / 60)
            let min = Math.floor(value % 60)
            return `${hour}h ${min}m`
        }
    },
}
</script>
<style lang="scss" scoped>
    .header{
            background: #E2E2E2;
            border-radius: 6px;
            display: flex;
            justify-content: flex-start;
            padding: 18px 35px;
            margin-bottom: 78px;
            text-align: left;
            a{
                background: #549DF2;
                border-radius: 100px;
                color: white;
                align-self: center;
                padding: 7px 14px;
                text-decoration: none;
                svg{
                    width:13px;
                    fill: white;
                }
            
            }
            div{
                margin-left:64px;
                &>p{
                    margin-bottom: 6px;
                }
                .title{
                    font-weight: 700;
                    font-size: 18px;
                    line-height: 21px;
                    
                }
                .tag{
                    font-weight: 400;
                    font-size: 18px;
                    line-height: 21px;
                }
            }
        }
    .movie-detail{
        padding-right:16px;
        &__img{
            
            &>div{
                width:100%;
                background-size: cover;
                background-position: center;
                height:495px;
                width:330px;
                border-radius: 12px;
            }
        }
        &__detail{
            margin-top:20px;
            .item{
                display: flex;
                justify-content: space-between;
                &__title{
                    font-weight: 700;
                    font-size: 16px;
                    line-height: 22px;
                }
                &__desc{
                    font-weight: 400;
                    font-size: 16px;
                    line-height: 22px;
                }

            }
        }
        &__overview{
            margin:53px 0px 80px 0px;
            text-align: left;
        }
        &__credit{
            text-align: left;
            .title{
                font-weight: 700;
                font-size: 18px;
                line-height: 22px;
            }
        }
    }
</style>