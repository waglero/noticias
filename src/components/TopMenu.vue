<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <router-link class="navbar-brand" to="/">Notícias</router-link>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
            </ul>
            <form class="form-inline my-2 my-lg-0">
            <input 
                v-bind:value="searchText"
                v-on="listeners" 
                class="form-control mr-sm-2" 
                type="search" 
                placeholder="Search" aria-label="Search">
            </form>
        </div>
    </nav>
</template>

<script>
export default {
    name: "TopMenu",
    data: function() {
        return {
            searchText: this.search
        }
    },
    props: {
        search: {
            type: String,
            default: ""
        }
    },
    computed: {
        listeners() {
            let self = this;
            return {
                ...this.$listeners,
                input: function (event) {
                    self.$emit('input', event.target.value);
                    self.searchText = event.target.value;
                }
            }
        }
    }
}
</script>

<style>
.navbar {
    box-shadow: 2px 2px 2px grey;
    font-weight: 700;
}
</style>
