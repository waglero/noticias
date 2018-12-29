<template>
    <div>
        <TopMenu v-model="searchText"/>
        <hr>
        <h1>Region: {{ $route.params.region }}</h1>
        <NewsList v-bind:newsLinksFiltered="newsLinksFiltered"/>
    </div>
</template>

<script>

import NewsList from '@/components/NewsList.vue'
import TopMenu from '@/components/TopMenu.vue'
import config from '../../vue.config.js'

export default {
    name: 'NewsPerRegion',
    data: function() {
        return {
            searchText: "",
            newsLinks: [],
        }
    },
    components: {
        NewsList, TopMenu
    },
    created: function() {
        let self = this;
        let request = new XMLHttpRequest();
        request.open("GET", config.baseUrl + "links.json");
        request.send();
        request.onreadystatechange = function() {
            if (this.readyState == 4) {
                self.newsLinks = JSON.parse(request.responseText);
            }
        }
    },
    computed: {
        newsLinksFiltered: function() {
            return this.newsLinks.filter(item => {
                let itemOk = true;
                if (! item.region.toLowerCase().includes(this.$route.params.region.toLowerCase())) {
                    itemOk = false;
                }
                if (! item.title.toLowerCase().includes(this.searchText.toLowerCase())) {
                    itemOk = false;
                }

                return itemOk;
            })
        }
    }
}
</script>

<style>
    h1 {
        color: #343a40;
        font-weight: 700;
    }
</style>
