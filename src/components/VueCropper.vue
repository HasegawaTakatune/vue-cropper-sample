<script setup lang="ts">
import Cropper from "cropperjs";

// javascript code
let cropper: any = null;

const cropImage = function (evt: any) {
  const files = evt.target.files;
  const file = files[0];
  const image = new Image();
  const reader = new FileReader();

  reader.onload = function (evt: any) {
    image.onload = function () {
      const canvas: any = document.getElementById("sourceCanvas");
      let ctx = canvas.getContext("2d");
      canvas.width = image.width;
      canvas.height = image.height;
      ctx.drawImage(
        image,
        0,
        0,
        image.width,
        image.height,
        0,
        0,
        canvas.width,
        canvas.height
      );

      cropper = new Cropper(canvas);
    };
    image.src = evt.target.result;
  };
  reader.readAsDataURL(file);
};
// document.getElementById("uploader")?.addEventListener("change", cropImage);
</script>

<template>
  <input type="file" id="uploader" @change="cropImage" />
  <div class="crop-area">
    <canvas id="sourceCanvas"></canvas>
  </div>
</template>

<style scoped>
img {
  display: block;

  max-width: 100%;

  background-color: white;
}
</style>
