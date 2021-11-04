<template>
    <div class='col'>
            <div class='row-lg-12'>
                <h1>Options</h1>
                <select class="form-select form-select-lg mb-4 p-5" aria-label=".form-select-lg">
                    <option selected>Select Model</option>
                    <option value="0">Drawer</option>
                    <option value="1">L-Shaped Kitchen</option>
                    <option value="2">Parallel Kitchen</option>
                    <option value="3">Italian Kitchen</option>
                </select>
            </div>
            <hr>
            <div class='row-lg-12'>
                <h1>Materials</h1>
            </div>
            <div class='row-lg-12'>
                <div class="row">
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(../assets/lighting/studio_1.png);">
                    </div>
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/studio_1.png);">
                </div>
            </div>

            <div class='row-lg-12'>
                <div class="row">
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/ballroom_1.png);">
                    </div>
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/studio_1.png);">
                    </div>
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/studio_2.png);">
                    </div>
                </div>
            </div>

            <hr>

            <div class='row-lg-12'>
                <h1>Lighting</h1> 
                <div class="row">
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(assets/lighting/ballroom_1.png);">
                    </div>
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/studio_1.png);">
                    </div>
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/studio_2.png);">
                    </div>
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/studio_3.png);">
                    </div>
                    <div class="col-lg-3 itemOption"
                    style="background-image: url(lighting/hall_1.png);">
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>
export default {
  name: 'Viewer3D',
  props: {
    msg: String
  },
  data() {
    return {
        loaded: false,
    }
  },
  methods: {

  },
  mounted() {
      this.loaded = true
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1 {
    text-align: left;
}

select{
    padding-left: 5px;
    border-radius: 1rem;
    color:black;
    width: 75%;
}

.itemOption{
    width: 50px;
    height: 50px;
    background: blanchedalmond;
    margin:5px;
}
</style>
