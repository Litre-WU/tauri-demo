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
          const textElement = document.createElement('div');
          const toneElement = document.createElement('div');
          const h5Element = document.createElement('h5');
          const phElement = document.createElement('p');


          divElement.setAttribute('class', 'content');
          textElement.setAttribute('class', 'text');
          toneElement.setAttribute('id', 'tone');
          imgElement.src = item.img;
          h5Element.textContent = item.song+' - '+item.singer;
          phElement.textContent = item.album;

          textElement.appendChild(h5Element);
          textElement.appendChild(phElement);
          divElement.appendChild(imgElement);
          divElement.appendChild(textElement);
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
<!--  <div class="content">-->
<!--    <img src="https://qpic.y.qq.com/music_cover/zQII3lJrGSNNoWObRlPoyng3yovJu21sRHSVvxDujsybVrrlTt9Nfw/300?n=1"-->
<!--         alt="测试">-->
<!--    <div class="text">-->
<!--      <h5>数到五 - By2</h5>-->
<!--      <p>数到五</p>-->
<!--    </div>-->
<!--    <div id="tone">-->
<!--      <div>HQ</div>-->
<!--      <div>SQ</div>-->
<!--      <div>FLAC</div>-->
<!--    </div>-->
<!--    <a href="" class="mplay">-->
<!--      <div>试听</div>-->
<!--    </a>-->
<!--  </div>-->
</template>

<style scoped>

</style>