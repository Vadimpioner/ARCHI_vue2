<template>
    <main
        class="AboutUs"
        :class="slideBackground"
        >
        <VueSlickCarousel v-bind="settings">
            <div class="container" v-for="item in slideContent" :key="item.h1">
                <section class="AboutUs__wrapper fd-c">
                    <h1 class="fz-96 fw700 green_heavy">{{item.h1}}</h1>
                    <div class="d-flex fd-r w100">
                        <div class="d-flex fd-c flex-1">
                            <span class="fz-18 fw600 green_heavy">{{ item.title_left }}</span>
                            <span class="fz-14 fw400 gray">
                                {{ item.descr_left }}
                            </span>
                        </div>
                        <div class="d-flex fd-c flex-1">
                            <span class="fz-18 fw600 green_heavy">{{ item.title_right }}</span>
                            <span class="fz-14 fw400 gray">
                                {{ item.descr_right }}
                            </span>
                        </div>
                    </div>
                    <div class="d-flex fd-r aic w100">
                        <common-button buttonClass="basic">
                            <span class="fz-18 fw600 font_futurademic white">
                                Read More
                            </span>
                        </common-button>
                        <common-button buttonClass="youtube">
                            <span class="fz-18 fw600 font_futurademic green_heavy">
                                View project
                            </span>
                        </common-button>
                    </div>
                </section>
            </div>
            <template #prevArrow="arrowOption" v-if="!fullMenu">
                <button>
                    <svg width="8" height="12" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="m6.5 1-5 5 5 5" stroke="#000" stroke-width="2"/></svg>
                    <div class="d-flex fd-r pos-a">
                        <span class="fz-18 fw400 font_futurademic">
                            {{ currentSlide = arrowOption.currentSlide + 1 }}
                        </span>
                        <div
                            class="this_progress pos-a"
                            :style="{width: ((arrowOption.currentSlide + 1) * 100) / (arrowOption.slideCount + 1) + '%'}"
                            >
                        </div>
                        <span class="fz-18 fw400 font_futurademic">{{ arrowOption.slideCount }}</span>
                    </div>
                </button>
            </template>
            <template #nextArrow v-if="!fullMenu">
                <button>
                    <svg width="8" height="12" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="m1 11 5-5-5-5" stroke="#000" stroke-width="2"/></svg>
                </button>
            </template>
        </VueSlickCarousel>
    </main>
</template>

<script>
    import VueSlickCarousel from 'vue-slick-carousel'
    import 'vue-slick-carousel/dist/vue-slick-carousel.css'
    export default {
        name: 'AboutUs',
        data: () => {
            return {
                settings: [
                    {
                        "lazyLoad": "ondemand",
                        arrows: true,
                        "infinite": false,
                    }
                ],
                currentSlide: null,
            }
        },
        props: {
            fullMenu: Boolean,
        },
        methods: {

        },
        computed: {
            slideContent() {
                return [
                    {
                        h1: 'Harmony',
                        title_left: 'Concept studio',
                        descr_left: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                        title_right: 'Everyday i’m',
                        descr_right: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                    },
                    {
                        h1: 'Testing',
                        title_left: 'Concept studio',
                        descr_left: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                        title_right: 'Everyday i’m',
                        descr_right: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                    },
                    {
                        h1: 'Buting',
                        title_left: 'Concept studio3',
                        descr_left: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                        title_right: 'Everyday i’m',
                        descr_right: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                    },
                    {
                        h1: 'Puding',
                        title_left: 'Concept studio4',
                        descr_left: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                        title_right: 'Everyday i’m',
                        descr_right: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                    },
                    {
                        h1: 'Omleting',
                        title_left: 'Concept studio5',
                        descr_left: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                        title_right: 'Everyday i’m',
                        descr_right: 'In our best design works, the Customer will find interiors in various styles, from strict modern minimalism to luxurious, richly decorated, from inexpensive, budgetary solutions to elite and unique.',
                    },
                ]
            },
            slideBackground() {
                switch (this.currentSlide) {
                    case 1:
                        return 'Harmony';
                    case 2:
                        return 'Testing';
                    case 3:
                        return 'Buting';
                    case 4:
                        return 'Puding';
                    case 5:
                        return 'Torting';
                    default:
                        return null
                }
            }
        },
        components: {
            VueSlickCarousel
        }
    }
</script>

<style lang="scss" scoped>
    .AboutUs {
        &::after {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background-repeat: no-repeat;
            background-size: cover;
            z-index: -1;
            box-shadow: 0 0 50px 25px rgba(221, 221, 221, 1);
            @keyframes fade1 {
                0% {
                    opacity: 0;
                    transform: scaleX(.97);
                }
                100% {
                    opacity: 1;
                    transform: scaleX(1);
                }
            }
            @keyframes fade2 {
                0% {
                    opacity: 0;
                    transform: scaleX(.97);
                }
                100% {
                    opacity: 1;
                    transform: scaleX(1);
                }
            }
        }
        &__wrapper {
            display: flex !important;
            max-width: 670px;
            padding: 5px;
            justify-content: center;
            @include adaptive_value('row-gap', 30, 15, 1, 320);
            .d-flex.fd-r.w100 {
                @include adaptive_value('column-gap', 50, 30, 1, 320);
                .d-flex.fd-c.flex-1 {
                    .fz-14.fw400.gray {
                        @include adaptive_value('margin-top', 16, 10, 1, 320);
                        @include adaptive_value('margin-bottom', 37, 20, 1, 320);
                    }
                }
            }
            .d-flex.fd-r.aic.w100 {
                @include adaptive_value('column-gap', 45, 20, 1, 320);
            }
        }


        .slick-slider {
            height: 100%;
        }
        .slick-arrow {
            position: absolute;
            bottom: -25px;
            left: 50%;
            transform: translate(-50%);
            padding: 5px;
            z-index: 2;
            svg {
                transition: opacity .3s, transform .3s;
            }
        }
        .slick-disabled {
            pointer-events: none;
            svg {
                opacity: .5;
            }
        }
        .slick-next {
            left: calc(50% + 150px);
            @media(min-width: 1201px) {
                &:hover {
                    svg {
                        transform: translateX(5px);
                    }
                }
            }
        }
        .slick-prev {
            left: calc(50% - 150px);
            @media(min-width: 1201px) {
                &:hover {
                    svg {
                        transform: translateX(-5px);
                    }
                }
            }
            .d-flex.fd-r.pos-a {
                top: 2px;
                left: 34px;
                width: 240px;
                span {
                    pointer-events: none;
                    position: absolute;
                    &:first-child {
                        left: 0;
                    }
                    &:last-child {
                        right: 0;
                    }
                }
                .this_progress.pos-a {
                    top: 10px;
                    left: 20px;
                    max-width: 200px;
                    height: 2px;
                    border-radius: 1px;
                    background: $green_heavy;
                    transition: width .7s;
                    &::after {
                        content: '';
                        position: absolute;
                        left: 0;
                        z-index: -1;
                        width: 200px;
                        height: 2px;
                        background: $gray_light;
                    }
                }
            }
        }

        .container {
            display: flex !important;
            height: calc(100vh - 188.8px);
        }
    }
    .AboutUs.Harmony {
        &::after {
            background-image: url('~/static/img/bg_slide_1.png');
            animation: .5s running fade1;
        }
    }
    .AboutUs.Testing {
        &::after {
            background-image: url('~/static/img/bg_slide_2.png');
            animation: .5s running fade2;
        }
    }
    .AboutUs.Buting {
        &::after {
            background-image: url('~/static/img/bg_slide_1.png');
            animation: .5s running fade1;
        }
    }
    .AboutUs.Puding {
        &::after {
            background-image: url('~/static/img/bg_slide_2.png');
            animation: .5s running fade2;
        }
    }
    .AboutUs.Torting {
        &::after {
            background-image: url('~/static/img/bg_slide_1.png');
            animation: .5s running fade1;
        }
    }
</style>
