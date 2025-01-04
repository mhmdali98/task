<template>
  <div class="container">
    <h1>search</h1>
    <input
      v-model="searchQuery"
      placeholder="type to search"
      class="search-box"
    />
    <p class="result-text">
      <b>{{ filterSearch.length }} result</b> were found
    </p>
    <div v-if="filterSearch.length" class="result-box">
      <div v-for="(item, index) in filterSearch" :key="index" class="">
        <h3 v-html="highlightFun(item.title)"></h3>
        <p class="date-text">{{ item.date }}</p>
        <p class="desc-text">{{ item.description }}</p>
        <div class="border"></div>
      </div>
    </div>
    <p v-else class="">no data found</p>
  </div>
</template>


<script setup>
const searchList = [
  {
    title: "i am mohammed ali",
    date: "Ocr 09 , 2025",
    description:
      "i am mohammed ali, i'm web developer, i have 26 years, my experience in this field 6 years, i live in iraq",
  },
  {
    title: "web developer",
    date: "Ocr 09 , 2025",
    description:
      "i am mohammed ali, i'm web developer, i have 26 years, my experience in this field 6 years, i live in iraq",
  },
  {
    title: "26 years old",
    date: "Ocr 09 , 2025",
    description:
      "i am mohammed ali, i'm web developer, i have 26 years, my experience in this field 6 years, i live in iraq",
  },
  {
    title: "6 years experience",
    date: "Ocr 09 , 2025",
    description:
      "i am mohammed ali, i'm web developer, i have 26 years, my experience in this field 6 years, i live in iraq",
  },
  {
    title: "living in iraq",
    date: "Ocr 09 , 2025",
    description:
      "i am mohammed ali, i'm web developer, i have 26 years, my experience in this field 6 years, i live in iraq",
  },
];

const searchQuery = ref("");

const filterSearch = computed(() => {
  if (!searchQuery.value.trim()) return searchList;

  return searchList.filter((list) =>
    list.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

const highlightFun = (content) => {
  if (!searchQuery.value.trim()) return content;

  const regex = new RegExp(`(${searchQuery.value})`, "gi");

  return content.replace(regex, "<mark>$1</mark>");
};
</script>

<style >
* {
  font-family: Arial, Helvetica, sans-serif;
}
.container {
  background-color: rgb(240, 240, 240);
  padding: 10px;
}
.search-box {
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 10px;
}
.result-text {
  padding: 10px 0;
}
.result-box {
  padding-top: 10px;
}
.date-text {
  color: #575757;
  font-size: 11px;
}
.desc-text {
  color: #373737;
  font-size: 12px;
}
.border {
  border-top: 2px solid #cacaca;
  padding: 10px 0;
  width: 50%;
}
</style>
