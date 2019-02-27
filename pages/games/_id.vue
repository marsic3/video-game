<template>
    <div>
        <div class="hero bg-grey-dark" :style="`background:url(${backgroundImage}); background-size:cover`">
            <div class="container mx-auto flex flex-col md:flex-row items-end pb-8 " style="height:350px">
                <div class="w-full md:w-1/4"></div>
                <div class="w-full md:w-3/4 md:ml-12">
                    <h1 class="font-heading text-white">{{game.name}}</h1>
                </div>
            </div>
        </div>
        <div class="container mx-auto flex flex-col md:flex-row">
            <div class="w-full md:w-1/4 -mt-16">
            <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="cover" class="mb-8">
            <div class="mb-4">
                <span class="font-semibold">Platforms:</span>
                <span v-for="platform in game.platforms" :key="platform.id">{{platform.name}}, </span>
            </div>
            <div class="mb-4">
              <span class="font-semibold">Released:</span>
              <span> {{ new Date(game.first_release_date).toDateString() }} </span>
            </div>
            <div class="mb-6">
                <a :href="getOfficialWebsite"> Official Website</a>
            </div>

            <div class="mb-10">
                <div class="text-5xl font-semibol">{{Math.round(game.total_rating)}} %</div>
                <span class="semi-bold">Overall Raiting</span>
            </div>
            </div>

            <div class="w-full md:w-3/4 md:ml-12 py-8 leading-normal">
                <div class="mb-12">{{game.summary}} </div>
                <div class="flex flex-wrap -mx-4">
                    <a href="#" v-for="screenshot in game.screenshots" 
                    :key="screenshot.cloudinary_id"
                    class="w-full md:w-1/4 px-4 md:mb-12 no-underline">
                        <img :src="screenshot.url.replace('t_thumb', 't_screenshot_med')" alt="screenshot">
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        computed: {
            getOfficialWebsite() {
                return this.game.websites[0].url
            },
            backgroundImage() {
                return this.game.screenshots[0].url.replace('t_thumb', 't_1080p')
            }
        },
        asyncData({
            params,
            error
        }) {
            return axios.get(`https://cors-anywhere.herokuapp.com/https://api-v3.igdb.com/games/${params.id}/?fields=name,summary,cover.url,platforms.name,first_release_date,websites.url,total_rating,screenshots.url`)
                .then((res) => {
                    return {
                        game: res.data[0]
                    }
                })
                .catch((e) => {
                    error({
                        statusCode: 404,
                        message: 'Post not found'
                    })
                })
        },
        head() {
            return {
                title: this.game.name + '| Video games'
            }
        }
    }
</script>

<style>
    
</style>
