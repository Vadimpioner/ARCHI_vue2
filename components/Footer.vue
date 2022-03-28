<template>
    <footer
        class="Footer"
        :class="{fullMenu : fullMenu}"
        >
        <div class="container">
            <div class="Footer__wrapper">
                <a
                    v-for="item in socialMedia"
                    :key="item.name"
                    :href="item.link"
                    target="_blank"
                    class="fz-16 fw600 font_futurademic"
                    >
                    {{ item.name }}
                </a>
            </div>
        </div>
    </footer>
</template>

<script>
    export default {
        name: 'Footer',
        computed: {
            socialMedia() {
                return [
                    {
                        link: '/#',
                        name: 'Facebook',
                    },
                    {
                        link: '/#',
                        name: 'Vkontakte',
                    },
                    {
                        link: '/#',
                        name: 'Behance',
                    },
                ]
            }
        },
        props: {
            fullMenu: Boolean
        }
    }
</script>

<style lang="scss" scoped>
    .Footer{
        &__wrapper {
            display: flex;
            width: max-content;
            @include adaptive_value('margin-bottom', 60, 30, 1, 320);
            @include adaptive_value('column-gap', 35, 10, 1, 320);
            .fz-16.fw600.font_futurademic {
                @media(min-width: 1201px) {
                    &:hover {
                        color: $green;
                    }
                }
            }
        }
    }
    .Footer.fullMenu {
        z-index: 5;
        .Footer__wrapper {
            width: 100%;
            justify-content: center;
            animation: 2s running fade;
            @keyframes fade {
                0% {
                    opacity: 0;
                }
                100% {
                    opacity: 1;
                }
            }
        }
    }
</style>
