<template>
  <div ref="map"></div>
</template>

<script>
import { Loader } from "@googlemaps/js-api-loader"
export default {
    methods: {
        addMarker(lat, lng){
            const marker = new google.maps.Marker({
                position: new google.maps.LatLng(lat, lng),
                map: this.map
            });
            this.markers.push(marker);
        },
        removeMarker(){
            this.markers.at(-1).setMap(null),
            this.markers.pop()
        }
    },
    props: ['center', 'zoom', 'locations'],
    mounted(){
        const loader = new Loader({
            apiKey: this.$config.googleApiKey,
            version: "weekly"
        });

        loader.load().then(() => {
            this.map = new google.maps.Map(this.$refs['map'], {
                center: this.center,
                zoom: this.zoom,
            });
            var i;
            for (i = 0; i < this.locations.length; i++){
                this.addMarker(this.locations[i][0], this.locations[i][1]);
            }
        });
    },
    data(){
        return {
            map: null,
            markers: []
        }
    },
    watch: {
        center(newCenter){
            this.map.panTo(newCenter);
        },
        zoom(newZoom){
            this.map.setZoom(newZoom);
        },
        locations(newLocations){
            if (newLocations.length > this.markers.length){
                this.addMarker(newLocations.at(-1)[0], newLocations.at(-1)[1]);
            } else if (newLocations.length < this.markers.length){
                this.removeMarker();
            }
        }

    }
}
</script>

<style scoped>
    div {
        height: 800px;
    }
</style>