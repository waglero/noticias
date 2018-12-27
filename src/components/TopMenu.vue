<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <<router-link class="navbar-brand" to="/">Notícias</router-link>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
            </ul>
            <form class="form-inline my-2 my-lg-0">
            <input 
                v-bind:value="search" 
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
                    self.search = event.target.value;
                }
            }
        }
    }
}
</script>

<style>
.navbar {
    border-radius: 5px;
}
</style>
