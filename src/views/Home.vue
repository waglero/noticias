<template>
  <div>
    <TopMenu v-model="searchText"/>
    <NewsList v-bind:newsLinksFiltered="newsLinksFiltered"/>
  </div>
</template>

<script>
// @ is an alias to /src
import NewsList from '@/components/NewsList.vue'
import TopMenu from '@/components/TopMenu.vue'
import config from '../../vue.config.js'

export default {
    name: 'home',
    data: function() {
        return {
            searchText: "",
            newsLinks: [],
        }
    },
    components: {
        TopMenu,
        NewsList
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
                return item.title.toLowerCase().includes(this.searchText.toLowerCase());
            })
        }
    }
}
</script>
