<template>
<div>
    <img src="https://logos-download.com/wp-content/uploads/2016/06/iTunes_logo_icon.png" alt="" height="150px" width="500px" class="img-fluid mx-auto" />
    <br />
    <br />
    <div class="row">
        <div class="col">
        </div>
        <div class="col">
            <input class="form-control ds-input " type=" text" v-model="keyword" placeholder="กรุณากรอกชื่อเพลง" />
            <br />
            <button @click="searchData" class="btn btn-danger">Search Music</button>
            <!--{{resultData}} -->
        </div>
        <div class="col">
        </div>
    </div>
    <br />
    <br />
    <div class="row">
        <div class="col-sm"></div>
        <div class="col-sm">
            <b-card-group columns>
                <div v-for="data in resultData" :key="data.trackId">
                    <b-card :title="data.title" :img-src="data.artworkUrl100" img-alt="Image" img-top tag="article" style="max-width: 25rem;" class="mb-2">
                        <b-card-text>{{ data.trackName }}</b-card-text>
                        <b-card-text>{{ data.artistName }}</b-card-text>
                        <audio controls >
                            <source :src="data.previewUrl" type="audio/mpeg" />
                        </audio>
                        <b-button :href="data.trackViewUrl" variant="danger">Play</b-button>
                    </b-card>
                </div>
            </b-card-group>
        </div>
        <div class="col-sm"></div>
    </div>
</div>
</template>

<script>
import axios from "axios";
export default {
    data() {
        return {
            resultData: null,
            keyword: "",
        };
    },
    methods: {
        searchData() {
            axios
                .get(
                    "https://itunes.apple.com/search?term=" + this.keyword + "&limit=15"
                )
                .then((response) => {
                    this.resultData = response.data.results;
                })
                .catch((err) => {
                    console.log(err);
                });
        },
    },
};
</script>

<style>
.card {
    background-image: url("https://data:image/jpeg;base64,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.google.co.th/url?sa=i&url=https%3A%2F%2Fwww.shutterstock.com%2Fth%2Fvideo%2Fclip-33079168-northern-lights-arctic-green-aurora-blue-sky&psig=AOvVaw3NGzlzKpMjEAdQDetG5euA&ust=1601297737645000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCMiWp6WxiewCFQAAAAAdAAAAABAottps://cdn.discordapp.com/attachments/746260527235334237/758702542690582558/BG.jpg");
}
</style>
