<template>
    <div class="TEMPLATE">
        <div class="TEMPLATE__wrapper">
            <Header
                style="flex: 0 0 auto"
                @full-menu="localFullMenu"
            />
            <transition name="fade">
                <Nuxt
                    style="flex: 1 0 auto"
                    :fullMenu="fullMenu"
                />
            </transition>
            <Footer
                style="flex: 0 0 auto"
                :fullMenu="fullMenu"
            />
        </div>
    </div>
</template>


<script>
    import Header from '../components/Header'
    import Footer from '../components/Footer'
    export default {
        components: {
            Header,
            Footer,
        },
        data: () => {
            return {
                fullMenu: null,
            }
        },
        methods: {
            localFullMenu(value) {
                this.fullMenu = value
            },
        },
        mounted() {
        },
    }
</script>

<style lang="scss" scoped>

.TEMPLATE {
    padding-right: 18px;
    overflow: overlay;
    &__wrapper {
        display: flex;
        flex-direction: column;
        height: 100vh;
    }
}
</style>
