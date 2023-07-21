<script setup>

const container = document.getElementById('app');

// 初始化数据
async function init() {
  fetch('http://10.2.106.77:8000/test', {
    'method': 'POST',
    body: JSON.stringify({test: 1}),
    headers: {'Content-Type': 'application/json'}
  })
      .then(response => response.json())
      .then(data => {
        // const container = document.getElementById('app');
        data.forEach(item => {
          const divElement = document.createElement('div');
          const imgElement = document.createElement('img');
          const paragraphElement = document.createElement('p');
          imgElement.src = item.img;
          paragraphElement.textContent = item.text;
          divElement.setAttribute('class', 'content')
          divElement.appendChild(imgElement)
          divElement.appendChild(paragraphElement);
          container.appendChild(divElement);
        });
      });
}

init();


// 下拉追加数据
async function fetchData(page) {
  fetch('http://10.2.106.77:8000/test', {
    'method': 'POST',
    body: JSON.stringify({page: page}),
    headers: {'Content-Type': 'application/json'}
  })
      .then(response => response.json())
      .then(data => {
        // const container = document.getElementById('app');
        data.forEach(item => {
          const divElement = document.createElement('div');
          const imgElement = document.createElement('img');
          const paragraphElement = document.createElement('p');
          imgElement.src = item.img;
          paragraphElement.textContent = item.text;
          divElement.setAttribute('class', 'content')
          divElement.appendChild(imgElement)
          divElement.appendChild(paragraphElement);
          container.appendChild(divElement);
        });
      });
}


document.addEventListener('DOMContentLoaded', () => {
  const element = document.getElementById('app').firstElementChild;
  element.addEventListener('scroll', () => {
    console.log(">>>");
    if (element.scrollTop + element.clientHeight >= element.scrollHeight) {
      console.log("????");
      // fetchData(2);
    }
  });
});

</script>

<template>
  <div class="content"><img src="https://www.litre.tk/image/header/home.jpg" alt="测试">
    <p>测试文本</p>
  </div>
  <div class="content"><img src="https://www.litre.tk/image/header/home.jpg" alt="测试">
    <p>测试文本</p>
  </div>
</template>

<style scoped>

</style>