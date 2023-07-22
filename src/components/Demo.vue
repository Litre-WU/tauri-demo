<script setup>

// 下拉追加数据
async function fetchData(page) {
  fetch('http://10.2.106.77:8000/test', {
    'method': 'POST',
    body: JSON.stringify({page: page}),
    headers: {'Content-Type': 'application/json'}
  })
      .then(response => response.json())
      .then(data => {
        const container = document.getElementById('app');
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


var page = 1;

fetchData(page);

window.addEventListener('scroll', () => {
  if ((window.innerHeight + window.scrollY) / document.body.offsetHeight >= 1) {
    page += 1;
    fetchData(page);
  }
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