<template>

    <router-link :to="{ name: 'movie-detail', params: { id: movie.id }}">

        <div class="movie-item">

            <div class="pic col-4" v-bind:style="{ backgroundImage: 'url(' + imageUrl + ')' }">
            </div>

            <div class="detail">
                <div class="title">{{movie.original_title}}</div>
                <div class="info">
                    <div class="date">
                        <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                            <rect width="16" height="16" fill="url(#pattern0)"/>
                            <defs>
                            <pattern id="pattern0" patternContentUnits="objectBoundingBox" width="1" height="1">
                            <use xlink:href="#image0_8_18" transform="translate(0 -0.015625) scale(0.03125)"/>
                            </pattern>
                            <image id="image0_8_18" width="32" height="33" xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAhCAQAAAASL2HaAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAAAmJLR0QA/4ePzL8AAAAHdElNRQfiAwoOOCiX8bOWAAAA8ElEQVRIx+2VTw7BUBCHv9afBVsShxHHEAcQcQaLLiyqV+AGIjiDOAzClkVbxkbrTUkpEpv+ZtHk9958b+a9ZAr/lvXgtGkBa6YJv0MTWDFLBzrILYbKH8a+kw7YIHi4CAfl7xFcPIRtOiBEKABnxGjPQjgDBYRQJxRv3yp96oBtrI2eHmHjAVsmnEx7Efd4r0BHVEEUC809ZgYcdQslA1YnfPK8FrV4t5ERbfQV4h0FlElc2kcyixpweTPLxk1aPqJgr44V/Ij1pXJADsgBPwIU4/lSopthHkCgreXDEH0Vcz0TK/RoZKh8x1j/F/6nK0D2d+Xdbd9cAAAAJXRFWHRkYXRlOmNyZWF0ZQAyMDE4LTAzLTEwVDE0OjU2OjQwKzAwOjAwQn9tOgAAACV0RVh0ZGF0ZTptb2RpZnkAMjAxOC0wMy0xMFQxNDo1Njo0MCswMDowMDMi1YYAAAAASUVORK5CYII="/>
                            </defs>
                        </svg>
                        {{movie.release_date}}
                    </div>
                    <div class="genre">
                        <span v-for="genre in genresOfMovie" :key="genre.id">
                            {{ genre.name}}
                        </span>
                    
                    </div>
                </div>
            </div>

        </div>

    </router-link>
    
</template>
<script>
export default {
    props:['movie', 'genres'],
    computed:{
        genresOfMovie(){
            let genresList=[]
            if(this.movie && this.genres)
            {
                let genresTitle = this.movie.genre_ids.map(m => this.genres.filter(g => g.id === m))
                genresTitle.map(genre => genre.map(g => genresList.push(g)))
                return genresList
            }
        },
        imageUrl(){
            return `https://image.tmdb.org/t/p/w500${this.movie.backdrop_path}`
        }
    }
}
</script>
<style lang="scss" scoped>
    a{
        text-decoration: none;
    }
    .movie-item{
        width:295px;
        background-color: #F1F1F1;
        border: 1px solid #C4C4C4;
        border-radius: 6px;
        padding: 3px;
        margin:35px 67px;
        display: flex;
        color:black;
        .pic{
            width: 128px;
            height:189px;
            overflow: hidden;
            background-image: url(https://image.tmdb.org/t/p/w500/fOy2Jurz9k6RnJnMUMRDAgBwru2.jpg);
            background-size: cover;
            background-position: center;
            border-radius: 6px 0px 0px 6px;
        }
        .detail{
            margin:14px;
            text-align: left;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            .title{
                font-weight: 700;
                font-size: 16px;
                line-height: 19px;
            }
            .info{
                font-weight: 400;
                font-size: 12px;
                line-height: 14px;
                .genre{
                    display: flex;
                    flex-wrap: wrap;
                    color: #505050;
                    span{
                        margin-right:4px;
                    }
                    span:not(:last-child):after{
                        display: inline-block;
                        content: "";
                        border-radius: 0.375rem;
                        height: 0.25rem;
                        width: 0.25rem;
                        margin-right: 0.5rem;
                        background-color: black;
                        margin-left: 4px;
                    }
                }
                .date{
                    color: #4E4E4E;
                    margin-bottom: 14px;
                }
            }
        }
    }
</style>