<template>
<div class="container mx-auto pt-2">
    <div class="row">
        <div class="w-full max-w-screen-xl mx-auto px-auto">
            <p class="text-red-500 text-sm">Ketik Hadis apa yang akan kamu cari, kemudian klik Cari Hadis</p>
            <div class="w-full max-w-screen-xl">
                <div class="flex items-center border-b border-teal-500 py-2">
                    <input class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" type="text" v-model="cariHadis" placeholder="Niat" v-on:keyup.enter.prevent="clickCari">
                    <button v-bind:class="{ 'animate-pulse': proseCari }" @click.prevent="clickCari" class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded" type="button">
                        {{ textCari }}
                    </button>
                    <button v-bind:class="{ 'hidden': !proseCari }" @click="stopCari" class="flex-shrink-0 bg-red-500 hover:bg-red-700 border-red-500 hover:border-red-700 text-sm border-4 text-white py-1 px-2 rounded" type="button">
                        X
                    </button>
                </div>
            </div>
            <div v-if="proseCari" class="mt-4 border border-gray-300 shadow rounded-md p-4 max-w-screen-xl">
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
            <div v-for="(Hadis,index) in Hadis.data" :key="index" class="mt-2 border-green-400 border-2 rounded-sm">
                <a class="-m-3 p-3 flex items-start space-x-4 rounded-lg hover:bg-gray-50 transition ease-in-out duration-150">
                    <svg class="flex-shrink-0 h-6 w-6 text-tael-300" x-description="Heroicon name: view-grid" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"></path>
                    </svg>
                    <div class="row w-full">
                        <div class="space-y-1 mb-2">
                            <p class="text-base leading-6 font-medium text-gray-900">
                                {{Hadis.kitab}}
                            </p>
                            <p class="text-sm leading-5 text-gray-500">
                                Nomor Hadis.
                            </p>
                        </div>
                        <div class="grid grid-cols-3 gap-4 pb-3 items-center">
                            <nuxt-link :to="{path: '/'+Hadis.kitab+'/'+idKitab}" type="button" class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded mr-2" v-for="(idKitab,index) in Hadis.id" :key="index">{{idKitab}}</nuxt-link>
                        </div>
                    </div>

                </a>
            </div>
            <div v-if="failedFind" class="lg:text-center pt-3">
                <p class="text-base leading-6 text-indigo-600 font-semibold tracking-wide uppercase">Respone Server</p>
                <h3 class="mt-2 text-3xl leading-8 font-extrabold tracking-tight text-red-700 sm:text-4xl sm:leading-10">
                    Hadis Tidak Di Temukan !!!
                </h3>
                <p class="mt-4 max-w-2xl text-xl leading-7 text-gray-500 lg:mx-auto">
                    ketik kata pencarian Hadis dengan ejaan yang benar !!!
                </p>
            </div>
            <div v-if="serverUnrespone" class="lg:text-center pt-3">
                <p class="text-base leading-6 text-indigo-600 font-semibold tracking-wide uppercase">Server Tidak Merespone</p>
                <h3 class="mt-2 text-3xl leading-8 font-extrabold tracking-tight text-gray-900 sm:text-4xl sm:leading-10">
                    Silahkan Cek Koneksi Internet Anda !!!
                </h3>
                <p class="mt-4 max-w-2xl text-xl leading-7 text-gray-500 lg:mx-auto">
                    cara mudah mencari Hadis di carihadis.my.id
                </p>
            </div>
        </div>
    </div>
</div>
<!-- coba -->
</template>

<script>
export default {
    name: 'Index',
    data() {
        return {
            proseCari: false,
            cariHadis: '',
            textCari: 'Cari Hadis',
            Hadis: [],
            failedFind: false,
            serverUnrespone: false
        }
    },
    methods: {
        clickCari() {
            if (this.cariHadis && this.proseCari == false) {
                this.proseCari = true
                this.failedFind = false
                this.serverUnrespone = false
                this.textCari = 'Proses Mencari Hadis'
                this.getHadis()
            }
        },
        stopCari() {
            this.proseCari = false
            this.textCari = 'Cari Hadis'
        },
        async getHadis() {
            this.Hadis = []
            const proxyurl = "https://cors-anywhere.herokuapp.com/";
            const url = "https://api.carihadis.com/" + "?q=" + this.cariHadis; // site that doesn’t send Access-Control-*
            await fetch(url) // https://cors-anywhere.herokuapp.com/https://example.com
                .then(response => response.text())
                .then(contents => {
                    //console.log(contents)
                    this.proseCari = false
                    this.textCari = 'Cari Hadis'
                    this.Hadis = JSON.parse(contents)
                    //console.log(JSON.parse(contents))
                    if (JSON.parse(contents).data == null) {
                        //alert('Data Tidak Di Temukan')
                        this.failedFind = true
                    }
                })
                .catch((e) => {
                  this.serverUnrespone = true
                })
        },
        async nomorHadis(kitab) {
            //alert(kitab)
            if (process.server) {
                return
            } else {
                return this.Hadis.filter((kitab) => {
                    console.log(this.Hadis.match(this.Hadis))
                    return this.Hadis.match(this.Hadis)
                })
            }

        }
    }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.animation.spin {
    animation: spin 1s linear infinite;

    @keyframes spin {
        from {
            transform: rotate(0deg);
        }

        to {
            transform: rotate(360deg);
        }
    }
}
</style>
