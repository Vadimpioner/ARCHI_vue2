<template>
    <div class="CommonSearch">
        <svg
            class="c-p"
            :style="{pointerEvents: valueInput == '' && searchInput ? 'none' : null}"
            @click="showSearchInput"
            width="20"
            height="20"
            fill="none"
            alt="search"
            xmlns="http://www.w3.org/2000/svg">
            <path d="m19.825 18.98-4.86-4.86a8.493 8.493 0 0 0 2.093-5.592C17.058 3.823 13.23 0 8.53 0 3.825 0 .002 3.827.002 8.528c0 4.7 3.827 8.527 8.528 8.527 2.137 0 4.093-.789 5.592-2.093l4.86 4.86c.116.116.27.178.422.178a.6.6 0 0 0 .421-1.02ZM1.195 8.528c0-4.045 3.29-7.33 7.33-7.33 4.045 0 7.33 3.29 7.33 7.33s-3.285 7.335-7.33 7.335c-4.04 0-7.33-3.29-7.33-7.335Z" fill="#444"/>
        </svg>
        <transition name="rightLeft">
            <div class="d-flex aic" v-if="searchInput">
                <input
                    type="text"
                    ref="searchInputRef"
                    v-model.trim="valueInput"
                    @keypress.enter="showSearchInput"
                    class="font_futurademic flex-1"
                    placeholder="What are you looking for?"
                >
                <svg
                    class="c-p"
                    @click="searchInput = false"
                    width="14"
                    height="14"
                    fill="none"
                    alt="searchClose"
                    xmlns="http://www.w3.org/2000/svg">
                    <path d="M1.235 13.592 13.588 1.367a.572.572 0 0 0 0-.815.587.587 0 0 0-.823 0L.412 12.778a.572.572 0 0 0 0 .814.587.587 0 0 0 .823 0Z" fill="#444"/><path d="M13.588 12.633 1.235.408a.587.587 0 0 0-.823 0 .572.572 0 0 0 0 .815l12.353 12.225a.587.587 0 0 0 .823 0 .572.572 0 0 0 0-.815Z" fill="#444"/>
                </svg>
            </div>
        </transition>
    </div>
</template>

<script>
    export default {
        name: 'CommonSearch',
        data:() => {
            return {
                searchInput: false,
                valueInput: '',
            }
        },
        methods: {
            showSearchInput() {
                if(this.valueInput == '' && !this.searchInput) {
                    this.searchInput = true;
                    setTimeout(() => {
                        this.$refs.searchInputRef.focus();
                    }, 500)
                }
                else if(this.valueInput !== '' && this.searchInput) {
                    alert(this.valueInput)
                    this.valueInput = '';
                }
            },
        },
        watch: {
            searchInput: function(value) {
                this.$emit('search-input', value)
            }
        }
    }
</script>

<style lang="scss" scoped>
    .CommonSearch {
        width: max-content;
        position: relative;
        display: flex;
        align-items: center;
        padding: 15px 0;
        overflow: hidden;
        @include adaptive_value('padding-left', 20, 10, 1, 320);
        @include adaptive_value('padding-right', 20, 10, 1, 320);
        &:after, &:before {
            content: '';
            position: absolute;
            height: 20px;
            width: 1px;
            background: $gray_light;
        }
        &::after {
            left: 0;
        }
        &::before {
            right: 0;
        }
        svg[alt=search],[alt=searchClose] {
            path {
                transition: fill .3s;
            }
            @media(min-width: 1201px) {
                &:hover {
                    path {
                        fill: $green;
                    }
                }
            }
        }
        .d-flex.aic {
            width: 580px;
            opacity: 1;
            transition: width .5s, opacity .3s;
            input {
                border: unset;
                padding: 0;
                background: transparent;
            }
        }
    }
</style>
