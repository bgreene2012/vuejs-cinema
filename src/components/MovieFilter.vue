<template>
    <div id="movie-filter">
        <h2>Filter results</h2>
        <div class="filter-group">
            <check-filter v-for="genre in genres" v-bind:title="genre" v-on:check-filter="checkFilter"></check-filter>
        </div>
        <check-filter></check-filter>
    </div>
</template>

<script>
    import genres from '../util/genres';
    import CheckFilter from './CheckFilter.vue';

    export default {
        data() {
            return {
                genres
            };
        },
        methods: {
            checkFilter(category, title, checked) {
                this.$emit('check-filter', category, title, checked);
            }
        },
        components: {
            'check-filter': {
                data() {
                    return {
                        checked: false
                    };
                },
                props: [ 'title' ],
                template: `<div v-on:click="checkFilter" v-bind:class="{ 'check-filter':true, active: checked }">
                                <span class="checkbox"></span>
                                <span class="check-filter-title">{{ title }}</span>
                            </div>`,
                methods: {
                    checkFilter() {
                        this.checked = !this.checked;
                        this.$emit('check-filter', 'genre', this.title, this.checked);
                    }
                }
            }
        }
    }
</script>

<style>

</style>