<script setup>

// 下拉追加数据
async function fetchData(page) {
  fetch("https://merry-jawfish-43540.kv.vercel-storage.com", {
    method: 'POST',
    body: '["GET", "testData"]',
    headers: {
      Authorization: 'Bearer AaoUASQgYTRhNzYxOGMtZGQzYS00M2Y4LWE5MDAtOGVjNTFmMTYwNDljNDg5ZmVhNmMyNDQ5NDEwZmIzYjU1YmEyOTIxZGQ5NDE='
    },
  })
      .then(response => response.json())
      .then(data => {
        console.log(eval(data.result));
        const container = document.getElementById('app');
        eval(data.result).forEach(item => {
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
<!--  <div class="content"><img src="https://www.litre.tk/image/header/home.jpg" alt="测试">-->
<!--    <p>测试文本</p>-->
<!--  </div>-->
<!--  <div class="content"><img src="https://www.litre.tk/image/header/home.jpg" alt="测试">-->
<!--    <p>测试文本</p>-->
<!--  </div>-->
</template>

<style scoped>

</style>