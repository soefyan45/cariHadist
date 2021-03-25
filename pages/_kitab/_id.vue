<template>
<div class="container mx-auto">
    <div v-if="serverUnrespone" class="lg:text-center pt-3">
        <p class="text-base leading-6 text-indigo-600 font-semibold tracking-wide uppercase">Server Tidak Merespone</p>
        <h3 class="mt-2 text-3xl leading-8 font-extrabold tracking-tight text-gray-900 sm:text-4xl sm:leading-10">
            Silahkan Cek Koneksi Internet Anda !!!
        </h3>
        <p class="mt-4 max-w-2xl text-xl leading-7 text-gray-500 lg:mx-auto">
            cara mudah mencari hadis di carihadis.my.id
        </p>
    </div>
    <div v-if="hadistEmpty" class="lg:text-center pt-3">
        <p class="text-base leading-6 text-indigo-600 font-semibold tracking-wide uppercase">Respone Server</p>
        <h3 class="mt-2 text-3xl leading-8 font-extrabold tracking-tight text-red-700 sm:text-4xl sm:leading-10">
            Hadis Tidak Di Temukan !!!
        </h3>
        <p class="mt-4 max-w-2xl text-xl leading-7 text-gray-500 lg:mx-auto">
            ketik kata pencarian hadis dengan ejaan yang benar !!!
        </p>
        <button type="button">Kembali</button>
    </div>
    <div class="flex justify-between">
        <div class="row">
            <h1>Kitab: {{this.$route.params.kitab}}</h1>
            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-red-100 text-red-800 mb-3">
                No. Hadis {{ this.$route.params.id }}
            </span>
        </div>
        <div class="row">
            <nuxt-link to="/" class="inline-block border border-white rounded py-2 px-4 bg-teal-500 text-white mr-2">
                Kembali
            </nuxt-link>
        </div>
    </div>
    <div v-if="loadingHadist" class="mt-4 border border-gray-300 shadow rounded-md p-4 max-w-screen-xl">
        <div class="animate-pulse flex space-x-4">
            <div class="flex-1 space-y-4 py-1">
                <div class="h-4 bg-gray-400 rounded w-3/4"></div>
                <div class="space-y-2">
                    <div class="h-4 bg-gray-400 rounded"></div>
                    <div class="h-4 bg-gray-400 rounded w-5/6"></div>
                </div>
            </div>
        </div>
        <div class="animate-pulse flex space-x-4">
            <div class="flex-1 space-y-4 py-1">
                <div class="h-4 bg-gray-400 rounded w-3/4"></div>
                <div class="space-y-2">
                    <div class="h-4 bg-gray-400 rounded"></div>
                    <div class="h-4 bg-gray-400 rounded w-5/6"></div>
                </div>
            </div>
        </div>
    </div>
    <div v-for="(hadis,index) in bacaHadist.data" :key="index">
        <div class="text-2xl mb-4 text-green-400 justify-end" v-html="hadis.nass">
        </div>
        <div class="text-xl ustify-between" v-html="hadis.terjemah">
        </div>
    </div>
</div>
</template>
<script>
export default {
    name: 'id',
    data() {
        return {
            bacaHadist: [],
            serverUnrespone: false,
            hadistEmpty: false,
            loadingHadist: true,
        }
    },
    created() {
        //console.log('created true'),
        this.serverUnrespone = false
        this.getHadist()
    },
    methods: {
        async getHadist() {
            this.bacaHadist = []
            const proxyurl = "https://cors-anywhere.herokuapp.com/";
            const url = "https://api.carihadis.com/" + "?kitab=" + this.$route.params.kitab + '&id=' + this.$route.params.id; // site that doesn’t send Access-Control-*
            await fetch(url) // https://cors-anywhere.herokuapp.com/https://example.com
                .then(response => response.text())
                .then(contents => {
                    //console.log(contents)
                    this.loadingHadist = false
                    if (JSON.parse(contents).data.length == 0) {
                        this.hadistEmpty = true
                        return
                    }
                    this.bacaHadist = JSON.parse(contents)
                    console.log(JSON.parse(contents))

                })
                .catch((e) => {
                    this.serverUnrespone = true
                })
        },
    }
}
</script>

<style>

</style>
