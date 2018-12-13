<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <p>
            For a guide and recipes on how to configure / customize this project,<br>
            check out the
            <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
        </p>
        <h3>Installed CLI Plugins</h3>
        <ul>
            <button v-on:click="poiExport()">PoiExport</button>
            <button v-on:click="easyExcelExport()">EasyExcelExport</button>
            <button v-on:click="easyExcelExportUrl()">EasyExcelExportUrl</button>
2        </ul>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        methods: {
            poiExport: function () {
                axios
                    .get(
                        'http://localhost:25001/poi/export',
                        {
                            responseType:'arraybuffer',
                            headers: {'Content-Type': 'multipart/form-data;charset=UTF-8'}
                        }
                    )
                    .then(res => {
                        var blob = new Blob([res.data], {type: 'application/vnd.ms-excel;charset=utf-8'})
                        var downloadElement = document.createElement('a');
                        var href = window.URL.createObjectURL(blob);
                        downloadElement.href = href;
                        downloadElement.download = '导出文件.xls';
                        document.body.appendChild(downloadElement);
                        downloadElement.click();
                        document.body.removeChild(downloadElement);
                        window.URL.revokeObjectURL(href);
                        /*var blob = new Blob([res.data], { type: 'application/vnd.ms-excel' })
                        var objectUrl = URL.createObjectURL(blob)
                        window.location.href = objectUrl*/
                    })
                    .catch(error => {
                        console.log(error)
                    })
            },
            easyExcelExport: function () {
                axios
                    .get(
                        'http://localhost:25001/easyExcel/export',
                        {
                            responseType:'arraybuffer',
                            headers: {'Content-Type': 'multipart/form-data;charset=UTF-8'}
                        }
                    )
                    .then(res => {
                        var blob = new Blob([res.data], {type: 'application/vnd.ms-excel;charset=utf-8'})
                        var downloadElement = document.createElement('a');
                        var href = window.URL.createObjectURL(blob);
                        downloadElement.href = href;
                        downloadElement.download = '导出文件.xls';
                        document.body.appendChild(downloadElement);
                        downloadElement.click();
                        document.body.removeChild(downloadElement);
                        window.URL.revokeObjectURL(href);
                        /*var blob = new Blob([res.data], { type: 'application/vnd.ms-excel' })
                        var objectUrl = URL.createObjectURL(blob)
                        window.location.href = objectUrl*/
                    })
                    .catch(error => {
                        console.log(error)
                    })
            },
            easyExcelExportUrl: function () {
                axios
                    .get(
                        'http://localhost:25001/easyExcel/exportUrl'
                    )
                    .then(res => {
                        var blob = new Blob([res.data], {type: 'application/vnd.ms-excel;charset=utf-8'})
                        var downloadElement = document.createElement('a');
                        var href = window.URL.createObjectURL(blob);
                        downloadElement.href = href;
                        downloadElement.download = '导出文件.xls';
                        document.body.appendChild(downloadElement);
                        downloadElement.click();
                    })
                    .catch(error => {
                        console.log(error)
                    })
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
