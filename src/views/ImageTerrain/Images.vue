<template>
    <div id="images">
        <drawer :show="drawerShow" :pos="pos" :tran="tran" @change-show="changeDrawerShow">
            <div class="layout" slot="drawer">
                <el-radio v-model="tmsCheck" @change="changeShow('tms')">天地图WG84影像</el-radio>
                <el-radio v-model="tmsCheck" @change="changeShow('tms')">天地图WebMercator影像</el-radio>
                <el-radio v-model="tmsCheck" @change="changeShow('tms')">天地图矢量</el-radio>
                <el-radio v-model="tmsCheck" @change="changeShow('tms')">本地影像服务</el-radio>
            </div>
        </drawer>
    </div>
</template>

<script >

export default {
    data() {
        return {
            drawerShow: false,
        }
    },
    watch: {

    },
    mounted() {
        this.$nextTick(function () {
        })
    },
    methods: {
        loadTDT() {
            let viewer = this.viewer;
            let layers = viewer.imageryLayers;
            //WG84
            layers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
                url: 'http://{s}.tianditu.com/img_c/wmts?service=WMTS&version=1.0.0&request=GetTile&tilematrix={TileMatrix}&layer=img&style={style}&tilerow={TileRow}&tilecol={TileCol}&tilematrixset={TileMatrixSet}&format=tiles',
                layer: 'img',
                style: 'default',
                format: 'tiles',
                tileMatrixSetID: 'c',
                credit: '天地图WG84影像服务',
                subdomains: ['t0', 't1', 't2', 't3', 't4', 't5', 't6', 't7'],
                maximumLevel: 19,
                tilingScheme: new Cesium.GeographicTilingScheme(),
                tileMatrixLabels: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18']
            }), 1);


            //WebMercator
            imageryLayers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
                url: 'http://{s}.tianditu.com/img_w/wmts?service=WMTS&version=1.0.0&request=GetTile&tilematrix={TileMatrix}&layer=img&style={style}&tilerow={TileRow}&tilecol={TileCol}&tilematrixset={TileMatrixSet}&format=tiles',
                layer: 'img',
                style: 'default',
                format: 'tiles',
                tileMatrixSetID: 'w',
                credit: '天地图WebMercator影像服务',
                subdomains: ['t0', 't1', 't2', 't3', 't4', 't5', 't6', 't7'],
                maximumLevel: 18
            }), 1);

        },

        changeDrawerShow(state) {
            this.drawerShow = state;
        },
    }
}
</script>

<style >
.el-menu-cesium {
    z-index: 999;
}
</style>