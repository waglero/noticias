<template>
    <div id="newsLinks">
        <div class="row">
            <div class="col-sm-6 col-md-3" v-for="(item, key) in newsLinksFiltered">
                <div v-bind:key="key" class="box">
                    <h5><a style="color: #007bff;" target="_blank" v-bind:href="item.url">{{ item.title }}</a></h5>
                    <div class="links">
                    <router-link class="badge badge-info" :to="{name: 'city', params: {city: item.city}}">{{ item.city }}</router-link>
                    <router-link class="badge badge-light" :to="{name: 'region', params: {region: item.region }}">{{ item.region }}</router-link >
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["newsLinksFiltered"],
    name: "NewsList"
}
</script>

<style>
.box {
    height: 100px;
    padding:10px;
    background-color: #343a40;
    margin-top: 10px;
    border-radius: 5px;
}
.links {
    margin-top:30px;
}
.links > a {
    margin-left:5px;
}
#newsLinks {
    margin-top: 18px;
}
</style>
