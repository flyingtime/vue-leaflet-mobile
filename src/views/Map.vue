<template>
    <div class="full-height">
        <l-map :zoom="zoom" :center="center" :min-zoom="minZoom" :max-zoom="maxZoom" :attributionControl="attributionControl">
            <l-tilelayer :url="url" :attribution="attribution"></l-tilelayer>
            <l-marker :position="center" :title="$t(cityName)" :opacity="opacity" :draggable="draggable">
                <l-popup :content="$t(cityName)"></l-popup>
            </l-marker>
        </l-map>
    </div>
</template>

<script>

import { mapState, mapMutations, mapGetters } from 'vuex'
import locateControl from 'leaflet.locatecontrol'

export default {
    data() {
        return {
            zoom: 9,
            minZoom: 1,
            maxZoom: 18,
            url: 'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
            attribution: 'brandon.xiang',
            title: 'test-marker',
            opacity: 1,
            draggable: false,
            attributionControl: false,
        };
    },

    computed: {
        ...mapGetters([
            'center',
            'cityName',
        ])
    },

    mounted() {
        this.SET_HEADER({
            title:this.$t('Map'),
            rightOption:{ show: true, name: '城市', link: 'cities' },
        })
        this.addControl(new locateControl())
    },

    methods: {
        ...mapMutations(['SET_HEADER', 'addControl'])
    }
}

</script>

<style>
@import "https://cdn.bootcss.com/leaflet/1.0.3/leaflet.css";
@import "~leaflet.locatecontrol/dist/L.Control.Locate.css";
@import "//maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css";

#map {
    width: 100%;
    height: 100%;
}
</style>
