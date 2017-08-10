<template>
    <nav aria-label="Navigation" :class="align">
        <ul class="pagination m-t-5">

            <li :class="(current == 1) ? 'disabled' : '' " v-if="arrows">
                <a v-on:click.prevent="onPaginatorClicked(prev_page)" aria-label="Previous">
                    <span aria-hidden="true">&laquo;</span>
                </a>
            </li>

            <li v-for="pageNumber in total_pages"
                v-if="Math.abs(pageNumber - current) < offset || pageNumber == last || pageNumber == 1"
                :class="(pageNumber == current) ? 'active' : ''">

                <a v-on:click.prevent="onPaginatorClicked(pageNumber)"
                   aria-label="Previous"
                   :class="linkClass(pageNumber)">
                    <span aria-hidden="true">{{ pageNumber }}</span>
                </a>

            </li>

            <li :class="(current == last) ? 'disabled' : '' " v-if="arrows">
                <a v-on:click.prevent="onPaginatorClicked(next_page)" aria-label="Next">
                    <span aria-hidden="true">&raquo;</span>
                </a>
            </li>

        </ul>
    </nav>
</template>

<script>
    export default {
        props: {
            'current': {
                required: true
            },
            'last': {
                required: true
            },
            'offset': {
                default: 3
            },
            'align': {
                default: 'text-center'
            },
            'arrows': {
                default: true
            }
        },

        methods: {
            onPaginatorClicked: function (page) {
                this.$emit('paginate', page);
            },

            linkClass: function (pageNumber) {
                return {
                    'current': this.current === pageNumber,
                    'last': (pageNumber == this.last && Math.abs(pageNumber - this.current) > this.offset),
                    'first': (pageNumber == 1 && Math.abs(pageNumber - this.current) > this.offset)
                }
            }
        },

        computed: {

            total_pages: function () {
                return Math.ceil(this.last);
            },

            next_page: function () {

                if (this.current) {
                    return parseInt(this.current) + 1;
                } else {
                    return 2;
                }

            },

            prev_page: function () {

                if (this.current) {
                    return parseInt(this.current) - 1;
                } else {
                    return 1;
                }

            },

        },
    }
</script>

<style scoped>

    a.first::after {
        content: '...'
    }

    a.last::before {
        content: '...'
    }

</style>
