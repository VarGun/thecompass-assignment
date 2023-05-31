<template>
  <div class="SearchBar">
    <input
      placeholder="지역명, 지하철역, 트레이너"
      @keydown="keyDownHandler"
      @change="onChangeHandler"
    />
    <img src="../../public/Images/Search.svg" />
  </div>
</template>

<script>

export default {
  name: "SearchBar",
  data() {
    return {
      aToken: "Token " + process.env.VUE_APP_AUTH_TOKEN,
      searchText: "",
    };
  },
  props: ['fetchData','pageNum','resetPageNum'],
  methods: {
    keyDownHandler: function (event) {
      if (event.keyCode === 13) {
        this.searchText = event.target.value;
        console.log("child : ",this.searchText);
        this.$emit(`update-searchName`, this.searchText);
        this.resetPageNum();
        this.fetchData();
      }
    },
    onChangeHandler(event) {
      this.searchText = event.target.value;
    },

  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.SearchBar {
  width: 480px;
  display: flex;
  height: 48px;
  padding: 16px;
  justify-content: space-between;
  border-bottom: 1px solid #f5f5f5;
  border-radius: 6px 6px 0px 0px;

  > input {
    flex: 1;
    outline: none;
    border: none;
    font-size: 16px;
    &::placeholder {
      color: #98a5b3;
    }
  }
}
</style>
