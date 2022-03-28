<template>
    <header
        class="Header"
        :class="{fullMenu: fullMenu}"
        >
        <div class="container">
            <div class="d-flex fd-r jcsb aic w100 h100">
                <div class="d-flex jcsb aic">
                    <NuxtLink class="opacity" to="/">
                        <span class="fz-24 fw700">AR.CHI</span>
                    </NuxtLink>
                    <div class="d-flex fd-r pos-r">
                        <span
                            class="fz-16 fw600 ttu font_futurademic c-p"
                            :class="{active: active == 'rus'}"
                            @click="active = 'rus'"
                            >
                            rus
                        </span>
                        <span
                            class="fz-16 fw600 ttu font_futurademic c-p"
                            :class="{active: active == 'eng'}"
                            @click="active = 'eng'"
                            >
                            eng
                        </span>
                    </div>
                </div>
                <nav class="d-flex fd-r jcfe aic">
                    <transition name="fade">
                        <div
                            class="d-flex fd-r aic pos-r"
                            :class="{active: searchInput}"
                            >
                            <transition name="link">
                                <div
                                    class="d-flex fd-r wmc"
                                    v-if="!searchInput || searchInput && fullMenu">
                                    <NuxtLink
                                        class="fz-16 fw600 font_futurademic pos-r"
                                        v-for="item in navLinks"
                                        :key="item.name"
                                        :to="item.route"
                                        :class="[item.name.replace(' ', '_') + '_photo', item.position == 'right' ? 'right_position' : 'left_position']"
                                        @click.native="fullMenu = false"
                                        >
                                        {{ item.name }}
                                    </NuxtLink>
                                </div>
                            </transition>

                            <common-search
                                v-show="!fullMenu"
                                @search-input='localSearchInput'
                            />
                        </div>
                    </transition>
                    <div
                        class="this_humburger d-flex aic"
                        >
                        <transition name="fade">
                            <span
                                class="fz-16 fw600 font_futurademic"
                                v-if="fullMenu"
                                >
                                Close
                            </span>
                        </transition>
                        <div
                            class=" d-flex fd-c aie c-p"
                            :class="{active: fullMenu}"
                            @click="ShowFullMenu"
                            >
                            <span></span>
                            <span></span>
                            <span></span>
                        </div>
                    </div>
                </nav>
            </div>
        </div>
    </header>
</template>

<script>
    export default {
        name: 'Header',
        data: () => {
            return {
                active: 'rus',
                fullMenu: false,
                searchInput: null,
            }
        },
        methods: {
            ShowFullMenu() {
                this.fullMenu = !this.fullMenu;
                if(this.fullMenu === true) {
                    document.body.style.overflow = 'hidden';
                } else {
                    document.body.style.overflow = 'auto';
                }
            },
            localSearchInput(value) {
                this.searchInput = value
            },
        },
        computed: {
            navLinks() {
                return [
                    {
                        name: 'About us',
                        route: '/',
                        position: 'left'
                    },
                    {
                        name: 'Architecture',
                        route: '/architecture',
                        position: 'right'
                    },
                    {
                        name: 'Interior',
                        route: '/interior',
                        position: 'left'
                    },
                    {
                        name: 'Contact',
                        route: '/contact',
                        position: 'right'
                    },
                    {
                        name: 'Shop',
                        route: '/shop',
                        position: 'left'
                    },
                ]
            },
        },
        watch: {
            fullMenu: function(value) {
                this.$emit('full-menu', value)
            },
        },
    }
</script>

<style lang="scss" scoped>
    .Header {
        .d-flex.fd-r.jcsb.aic.w100.h100 {
            height: 100px;
            .d-flex.jcsb.aic {
                z-index: 5;
                @include adaptive_value('column-gap', 80, 30, 1, 320);
                .d-flex.fd-r.pos-r {
                    @include adaptive_value('column-gap', 20, 10, 1, 320);
                    &:after {
                        content: '';
                        position: absolute;
                        height: 80%;
                        width: 1px;
                        background: $black;
                        opacity: .5;
                        top: 50%;
                        transform: translateY(-50%);
                        @include adaptive_value('left', -40, -15, 1, 320);
                    }
                    .fz-16.fw600.ttu.font_futurademic {
                        padding: 5px 5px 2px 5px;
                        border: 1px solid transparent;
                        border-radius: 5px;
                        transition: border-color .3s, background .3s;
                        color: $black;
                        opacity: .5;
                        @media(min-width: 1201px) {
                            &:hover {
                                border-color: $green_light;
                            }
                        }
                    }
                    .fz-16.fw600.ttu.font_futurademic.active {
                        pointer-events: none;
                        opacity: 1;
                        background: $green_light;
                    }
                }
            }
            .d-flex.fd-r.jcfe.aic {
                overflow: hidden;
                @include adaptive_value('column-gap', 40, 10, 1, 320);
                .d-flex.fd-r.aic.pos-r {
                    overflow: hidden;
                    background-position-y: 100px;
                    .d-flex.fd-r.wmc {
                        @include adaptive_value('column-gap', 40, 10, 1, 320);
                        @include adaptive_value('margin-right', 40, 20, 1, 320);
                        .fz-16.fw600.font_futurademic.pos-r {
                            white-space: nowrap;
                            &::after {
                                content: '';
                                position: absolute;
                                width: 0;
                                height: 2px;
                                background: $black;
                                left: 50%;
                                bottom: -2px;
                                border-radius: 1px;
                                transition: left .3s, width .3s;
                            }
                            @media(min-width: 1201px) {
                                &:hover {
                                    &::after {
                                        left: 0;
                                        width: 100%;
                                    }
                                }
                            }
                        }
                        .fz-16.fw600.font_futurademic.pos-r.nuxtLinkActive {
                            pointer-events: none;
                            &::after {
                                left: 0;
                                width: 100%;
                            }
                        }
                    }
                }
                .d-flex.aic.pos-r.active {
                    .CommonSearch {
                        @include adaptive_value('padding-left', 10, 5, 1, 320);
                        @include adaptive_value('padding-right', 20, 10, 1, 320);
                        @include adaptive_value('column-gap', 10, 5, 1, 320);
                    }
                    &:after {
                        content: '';
                        position: absolute;
                        width: 100%;
                        height: 1px;
                        background: $gray_light;
                        left: 0;
                        bottom: 0;
                    }
                }
                .this_humburger {
                    z-index: 5;
                    .fz-16.fw600.font_futurademic {
                        transition: margin-right .3s, opacity .3s;
                        @include adaptive_value('margin-right', 14, 7, 1, 320);
                    }
                    .d-flex.fd-c.aie.c-p {
                        padding: 5px;
                        row-gap: 4px;
                        z-index: 2;
                        span {
                            width: 26px;
                            height: 2px;
                            background: $black;
                            border-radius: 1px;
                            box-sizing: initial;
                            transition: width .3s, opacity .3s, transform .3s;
                            &:last-child {
                                width: 18px;
                            }
                        }
                        @media(min-width: 1201px) {
                            &:hover {
                                span {
                                    &:first-child {
                                        width: 18px;
                                    }
                                }
                            }
                        }
                    }
                    .d-flex.fd-c.aie.c-p.active {
                        span {
                            width: 18px;
                            &:first-child {
                                transform: translateY(6px) rotate(45deg);
                            }
                            &:nth-child(2) {
                                opacity: 0;
                            }
                            &:last-child {
                                transform: translateY(-6px) rotate(-45deg);
                            }
                        }
                        @media(min-width: 1201px) {
                            &:hover {
                                span {
                                    &:first-child {
                                        transform: translateY(0) rotate(180deg);
                                    }
                                    &:last-child {
                                        transform: translateY(0) rotate(180deg);
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
    .Header.fullMenu {
        .d-flex.fd-r.jcsb.aic.w100.h100 {
            .d-flex.fd-r.jcfe.aic {
                .d-flex.fd-r.aic.pos-r {
                    position: absolute;
                    left: 0;
                    bottom: 0;
                    justify-content: center;
                    width: 100%;
                    height: 100%;
                    background-repeat: no-repeat;
                    background-size: cover;
                    background-position-y: 0;
                    background-color: rgb(245, 245, 245);
                    background-image: url('~/static/img/bg_fullMenu.png');
                    transition: background-position-y .3s, background-color .3s;
                    z-index: 4;
                    .d-flex.fd-r.wmc {
                        align-items: center;
                        flex-direction: column;
                        margin-right: 0;
                        position: relative;
                        @include adaptive_value('row-gap', 38, 10, 1, 320);
                        .fz-16.fw600.font_futurademic.pos-r {
                            position: initial;
                            font-family: inherit;
                            font-size: 48px;
                            color: $gray_light;
                            transition: font-size .3s, color .3s;
                            &::after {
                                content: unset;
                            }
                            &::before {
                                content: '';
                                position: absolute;
                                top: 48%;
                                transform: translateY(-50%);
                                width: 100%;
                                height: 316px;
                                pointer-events: none;
                                background-repeat: no-repeat;
                                background-size: contain;
                                opacity: 0;
                                transition: opacity .3s, top .3s;
                            }
                            @media(min-width: 1201px) {
                                &:hover {
                                    color: $green;
                                    &:before {
                                        opacity: 1;
                                        top: 50%;
                                    }
                                }
                            }
                        }
                        .fz-16.fw600.font_futurademic.pos-r.right_position {
                            &::before {
                                right: -120%;
                            }
                        }
                        .fz-16.fw600.font_futurademic.pos-r.left_position {
                            &::before {
                                left: -120%;
                            }
                        }
                        .fz-16.fw600.font_futurademic.pos-r.nuxtLinkActive {
                            color: $green;
                        }
                        .About_us_photo {
                            &::before {
                                background-image: url('~/static/img/link_photo/architecture_left.png');
                            }
                        }
                        .Architecture_photo {
                            &::before {
                                background-image: url('~/static/img/link_photo/interior_right.png');
                            }
                        }
                        .Interior_photo {
                            &::before {
                                background-image: url('~/static/img/link_photo/architecture_left.png');
                            }
                        }
                        .Contact_photo {
                            &::before {
                                background-image: url('~/static/img/link_photo/interior_right.png');
                            }
                        }
                        .Shop_photo {
                            &::before {
                                background-image: url('~/static/img/link_photo/architecture_left.png');
                            }
                        }
                    }
                }
            }
        }
    }
</style>
