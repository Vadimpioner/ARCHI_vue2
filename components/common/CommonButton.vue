<template>
    <button
        :disabled="disabled"
        :class="`CommonButton__${buttonClass}`"
        >
        <div class="d-flex pos-r" v-if="buttonClass == 'youtube'">
            <svg
                class="this_triangle"
                width="16"
                height="18"
                viewBox="0 0 16 18"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
                >
                <path
                    d="M15.5 8.13398C16.1667 8.51888 16.1667 9.48113 15.5 9.86603L2 17.6603C1.33334 18.0452 0.500001 17.564 0.500001 16.7942L0.500002 1.20577C0.500002 0.435972 1.33333 -0.0451548 2 0.339746L15.5 8.13398Z"
                    fill="#425A20"
                />
            </svg>

            <svg
                class="this_border pos-a"
                width="17"
                height="18"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
                >
                <path
                    d="M15.473 9.65 1.826 17.529a.75.75 0 0 1-1.125-.65V1.121A.75.75 0 0 1 1.826.47l13.647 7.88a.75.75 0 0 1 0 1.299Z"
                    stroke="#000"
                    stroke-width=".5"
                />
            </svg>
        </div>
        <slot name="default"></slot>
    </button>
</template>

<script>
    export default {
        name: 'CommonButton',
        methods: {
        },
        props: {
            disabled: {
                type: Boolean,
                required: false
            },
            buttonClass: {
                type: String,
                required: true,
                validator(val) {
                    return ["basic", "youtube"].includes(val);
                },
            },
        }
    }
</script>

<style lang="scss" scoped>
    .CommonButton__basic {
        position: relative;
        background: $green;
        border-radius: 5px;
        width: max-content;
        border: 1px solid transparent;
        @include adaptive_value('height', 46, 32, 1, 320);
        @include adaptive_value('padding-right', 57, 20, 1, 320);
        @include adaptive_value('padding-left', 57, 20, 1, 320);
        &::before {
            content: '';
            position: absolute;
            top: -1px;
            left: -2px;
            border: 1px solid $black;
            width: 100%;
            height: 100%;
            border-radius: 5px;
            transform: rotate(-2.09deg);
            transition: left .3s, transform .3s;
        }
        @media(min-width: 1201px) {
            &:hover {
                &:before {
                    left: -1px;
                    transform: rotate(0);
                }
            }
        }
    }

    .CommonButton__youtube {
        width: max-content;
        display: flex;
        column-gap: 7px;
        align-items: center;
        .d-flex.pos-r {
            .this_triangle {
                path {
                    transition: fill .3s;
                }
            }
            .this_border.pos-a {
                top: -0.5px;
                left: 0;
                transform: rotate(-12.08deg);
                transition: top .7s, left .7s, transform .7s;
            }
        }
        @media(min-width: 1201px) {
            &:hover {
                .d-flex.pos-r {
                    .this_border.pos-a {
                        top: 0;
                        left: .5px;
                        transform: rotate(0);
                    }
                    .this_triangle {
                        path {
                            fill: $red;
                        }
                    }
                }
            }
        }
    }
</style>
