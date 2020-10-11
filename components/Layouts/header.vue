<template>
<div>
    <header class="h-16 sm:flex sm:items-center sm:justify-between mx-5 lg:mb-1 mt-1">
        <div id="header">
            <div class="flex bg-teal-500 border-b border-teal-700 fixed top-0 inset-x-0 z-100 h-18 md:h-16 items-center">
                <div class="w-full max-w-screen-xl relative mx-auto px-6">
                    <div class="flex items-center py-5">
                        <div class="lg:w-1/4 xl:w-1/5 md:pr-2 lg:pr-8">
                            <div class="flex items-center">
                                <nuxt-link class="block lg:mr-4 no-underline" to="/">
                                    <h4 class="text-xl font-mono text-black">
                                        CariHadis.my.id
                                    </h4>
                                </nuxt-link>
                            </div>
                        </div>
                        <div class="flex flex-grow min-w-0 lg:w-3/4 xl:w-4/5">
                            <div class="w-full min-w-0 lg:px-6 xl:w-3/4 xl:px-12 pr-2">
                                <div class="relative">
                                    <!-- search form -->
                                </div>
                            </div>
                            <button @click.prevent="clickToggle" class="inline-flex items-center justify-center p-2 rounded-md lg:hidden text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:bg-gray-700 focus:text-white">
                                <!-- Menu open: "hidden", Menu closed: "block" -->
                                <svg class="block h-6 w-6" v-if="!toggleMenu" stroke="currentColor" fill="none" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                                </svg>
                                <!-- Menu open: "block", Menu closed: "hidden" -->
                                <svg class="fill-current w-4 h-4" v-if="toggleMenu" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
                                    <path d="M10 8.586L2.929 1.515 1.515 2.929 8.586 10l-7.071 7.071 1.414 1.414L10 11.414l7.071 7.071 1.414-1.414L11.414 10l7.071-7.071-1.414-1.414L10 8.586z"></path>
                                </svg>
                            </button>
                            <div class="hidden lg:flex lg:items-center lg:justify-between xl:w-1/4 px-6">
                                <div class="flex justify-start items-center text-gray-500">
                                    <nuxt-link class="block flex no-underline items-center font-semibold hover:text-black  text-gray-700" to="/about">
                                        About
                                    </nuxt-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>
    <div class="w-full lg:hidden lg:items-center lg:w-auto bg-teal-600 pt-2 md:pt-1 rounded-b-lg" v-if="toggleMenu">
        <div class="flex text-sm lg:flex-grow py-3 mr-2 justify-end" @click.prevent="unToggle">
            <nuxt-link class="inline-block border border-white rounded py-2 px-4 bg-teal-500 text-white mr-2" to="/">
                Home
            </nuxt-link>
            <nuxt-link class="inline-block border border-white rounded py-2 px-4 bg-teal-500 text-white mr-2" to="/about">
                About
            </nuxt-link>
        </div>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            toggleMenu: false
        }
    },
    methods: {
        clickToggle() {
            if (this.toggleMenu === false) {
                this.toggleMenu = true
                /* eslint no-useless-return: "error" */
                return true
            }
            if (this.toggleMenu === true) {
                this.toggleMenu = false
                /* eslint no-useless-return: "error" */
                return false
            }
        },
        unToggle() {
            console.log('false')
            this.toggleMenu = false
        }
    }
}
</script>
