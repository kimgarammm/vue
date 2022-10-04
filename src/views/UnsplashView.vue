<template>
  <TitleCont name1="UNSPLASH" name2="API" />
  <HeaderCont />
  <div class="unsplash__cont">
    <div class="container">
      <div class="unsplash__search">
        <form @submit.prevent="SearchImages()">
          <div class="container">
            <label for="search"></label>
            <input
              type="search"
              id="search"
              placeholder="검색하세요"
              v-model="search"
            />
            <button type="submit">검색</button>
          </div>
        </form>
      </div>
      <div class="unsplash__list">
        <ul>
          <li v-for="image in images" :key="image.id">
            <a :href="`https://unsplash.com/photos/${image.id}`">
              <img :src="image.urls.regular" :alt="image.desscription" />
              <span>{{ image.description }}</span>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </div>
  <ContactCont />
  <FooterCont />
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/HeaderCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },
  setup() {
    const images = ref([]);
    const search = ref("sky");

    const SearchImages = () => {
      fetch(
        `https://api.unsplash.com/search/photos?query=${search.value}&client_id=n1I0Rq5j3_YeAaay6pOldHW_vybPRxo3m931a-lo6DQ&per_page=30`
      )
        .then((response) => response.json())
        .then((data) => {
          images.value = data.results;
          search.value - "";
          console.log(images);
        })
        .catch((error) => console.log("error", error));
    };
    SearchImages();
    return {
      images,
      search,
      SearchImages,
    };
  },
};
</script>

<style scoped lang="scss">
.unsplash__cont {
  background-color: var(--black);
}
.unsplash__list ul {
  display: flex;
  flex-wrap: wrap;

  li {
    flex: 1 1 23%;
    margin: 1%;

    img {
      border-radius: 0.4em;
    }

    span {
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      color: #fff;
      color: var(--white);
      display: -webkit-box;
      font-family: SCoreDream;
      font-family: var(--subKor_font);
      overflow: hidden;
      padding-top: 10px;
      text-overflow: ellipsis;
    }
  }
}

.unsplash__search {
  background: var(--black);

  .container {
    position: relative;
  }

  h2 {
    color: var(--white);
    font-size: 40px;
    height: 0;
    text-indent: -9999px;
    width: 0;
  }

  input {
    background: var(--black);
    border: 2px solid var(--light_border);
    border-radius: 50px;
    color: #000;
    color: var(--white);
    margin: 0 1% 5%;
    padding: 1rem 3rem 1rem 2rem;
    width: 98%;
  }
  button {
    background: #fff;
    border: 0;
    border-radius: 50%;
    color: var(—black);
    font-family: var(—subKor_font);
    font-size: 12px;
    height: 40px;
    position: absolute;
    right: 22px;
    top: 9px;
    transition: opacity 0.3s ease;
    width: 40px;
  }
}
</style>
