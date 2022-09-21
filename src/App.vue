<script setup lang="ts">
import { ref } from "vue";

const imageData = ref<string | any>("");

function onChange(e: any) {
  // getting the input DOM element
  const input = e.target;

  // Ensure that you have a file before attempting to read it
  if (input.files && input.files[0]) {
    // create a new FileReader to read this image and convert to base format
    const fileReader = new FileReader();

    // Define a callback function to run, when FileReader finishes its job and the store the data
    fileReader.onload = (e: any) => {
      imageData.value = e.target.result;
    };

    //  Start the reader job and read file as a data url
    fileReader.readAsDataURL(input.files[0]);
  }
}

function removeImage() {
  imageData.value = "";
}
</script>

<template>
  <div>
    <h1>Vue TS Upload Image</h1>

    <label v-if="!imageData" class="bg-yellow-400 px-3 py-2 cursor-pointer" for="inputTag">
      Select a image
      <input type="file" id="inputTag" class="hidden" accept="image/*" @change="onChange" />
    </label>

    <div v-else>
      <img :src="imageData" />
      <button class="bg-red-400 px-3 py-2" @click.prevent="removeImage">Remove</button>
    </div>
  </div>
</template>
