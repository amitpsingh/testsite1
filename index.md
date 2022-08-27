---
title: Home
layout: default
---

# Simple JS Image Classifiers

Linked above are some examples of vision classifiers using JavaScript from [fast.ai](https://course.fast.ai) staff and students. Also, check out these other examples from students, along with the [fast.ai forums](https://forums.fast.ai) username of each contributor:

<input id="photo" type="file">
<div id="results"></div>
<script>
  async function loaded(reader) {
    const response = await fetch('https://hf.space/embed/amitpsingh/demo2/+/api/predict', {
      method: "POST", body: JSON.stringify({ "data": [reader.result] }),
      headers: { "Content-Type": "application/json" }
    });
    const json = await response.json();
    const label = json['data'][0]['confidences'][0]['label'];
    results.innerHTML = `<br/><img src="${reader.result}" width="300"> <p>${label}</p>`
  }
  function read() {
    const reader = new FileReader();
    reader.addEventListener('load', () => loaded(reader))
    reader.readAsDataURL(photo.files[0]);
  }
  photo.addEventListener('input', read);
</script>

