<template>
    <div id="movie-filter">
        <h2>Filter results</h2>
        <h3>By Time of Day</h3>
        <div class="filter-group">
            <check-filter v-for="time in times" category="time" v-bind:title="time" v-on:check-filter="checkFilter"></check-filter>
        </div>
        <h3>By Genre</h3>
        <div class="filter-group">
            <check-filter v-for="genre in genres" category="genre" v-bind:title="genre" v-on:check-filter="checkFilter"></check-filter>
        </div>
        <check-filter></check-filter>
    </div>
</template>

<script>
    import genres from '../util/genres';
    import times from '../util/times';

    export default {
        data() {
            return {
                genres,
                times
            };
        },
        methods: {
            checkFilter(category, title, checked) {
                this.$bus.$emit('check-filter', category, title, checked);
            }
        },
        components: {
            'check-filter': {
                data() {
                    return {
                        checked: false
                    };
                },
                props: [ 'title', 'category' ],
                template: `<div v-on:click="checkFilter" v-bind:class="{ 'check-filter':true, active: checked }">
                                <span class="checkbox"></span>
                                <span class="check-filter-title">{{ title }}</span>
                            </div>`,
                methods: {
                    checkFilter() {
                        this.checked = !this.checked;
                        this.$emit('check-filter', this.category, this.title, this.checked);
                    }
                }
            }
        }
    }
</script>

<style>

</style>