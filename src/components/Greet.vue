<script setup>
import {ref} from "vue";
import {invoke} from "@tauri-apps/api/tauri";


const greetMsg = ref("");
const name = ref("");

//初始问候
async function greet() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  greetMsg.value = await invoke("greet", {name: name.value});
}


const tip = ref("");

// 文件上传
async function uploadFiles() {
  const fileInput = document.getElementById('fileInput');
  const files = fileInput.files;
  const formData = new FormData();

  for (let i = 0; i < files.length; i++) {
    const file = files[i];
    // console.log('>>', file.name, file);
    formData.append("file", file)
  }
  fetch('http://10.2.106.77:8000/upload', {
    method: 'POST',
    headers: {
      'accept': 'application/json'
    },
    // body: JSON.stringify(formData)
    body: formData
  })
      .then(response => {
        console.log(response.json());
        if (response.ok) {
          console.log('File uploaded successfully!');
          tip.value = "上传成功！";
        } else {
          console.error('Error uploading file:', response.statusText);
          tip.value = "上传失败！";
        }
      })
      .catch(error => {
        console.error('Error uploading file:', error);
        tip.value = "上传失败！";
      });
}

</script>

<template>
  <form class="row" @submit.prevent="uploadFiles">
    <input type="file" placeholder="选择文件" id="fileInput" multiple/>
    <button type="submit" id="upload">上传</button>
  </form>
  <p id="tip">{{ tip }}</p>

<!--  <form class="row" @submit.prevent="greet">-->
<!--    <input id="greet-input" v-model="name" placeholder="Enter a name..."/>-->
<!--    <button type="submit">发送</button>-->
<!--  </form>-->
<!--  <p>{{ greetMsg }}</p>-->
</template>
