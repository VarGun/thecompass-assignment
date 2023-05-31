<template>
  <div id="app">
    <MainHeader class="Header"  />
    <div id="content">
      <KakaoMap id="kMap" @click="console.log(count)" />
      <div id="sideBar">
        <SearchBar
          @update-searchName="setSearchName"
          :searchName="searchName"
          :fetchData="fetchData"
          :pageNum="pageNum"
          @update-pageNum="setPageNum"
          :resetPageNum="resetPageNum"
        />
        <div id="fadeWrapper">
          <transition name="fade" v-show="orderingMode">
            <div id="orderingTrue">
              <LocationWrapper
                :orderingMode="orderingMode"
                @update-mode="changeOrderingMode"
              />
              <div id="TrainersContainer" v-for="i in results" :key="i.id" v-show="count !== 0">
                <TrainerCard :trainers="i" />
              </div>

              <div id="gotoPageContainer" v-show="count !== 0">
                <div
                  id="btnPrevious"
                  :style="{
                    color: pageNum === 1 ? '#6C7680' : '#ff8000',
                    border:
                      pageNum === 1 ? '1px solid #6C7680' : '1px solid #ff8000',
                  }"
                  @click="movePreviousPage"
                >
                  Previous
                </div>
                <div
                  id="btnNext"
                  :style="{
                    color: pageNum < endPage ? '#ff8000' : '#6C7680',
                    border:
                      pageNum < endPage
                        ? '1px solid #ff8000'
                        : '1px solid #6C7680',
                  }"
                  @click="moveNextPage"
                >
                  Next
                </div>
              </div>
            </div>
          </transition>
          <transition name="fade" v-show="!orderingMode">
            <FilterSetting
              :orderingMode="orderingMode"
              @update-mode="changeOrderingMode"
            />
          </transition>
        </div>
        <NoResult v-show="count === 0" />
      </div>
    </div>
  </div>
</template>

<script>
import MainHeader from "./components/MainHeader.vue";
import SearchBar from "./components/SearchBar.vue";
import LocationWrapper from "./components/LocationWrapper.vue";
import FilterSetting from "./components/FilterSetting.vue";
import TrainerCard from "@/components/TrainerCard.vue";
import NoResult from "@/components/NoResult.vue";
import KakaoMap from "@/components/KakaoMap.vue";
import axios from "axios";
export default {
  name: "app",
  data() {
    return {
      isInTrainers: false,
      orderingMode: true,
      results: [],
      searchName: "",
      pageNum: 1,
      count: 1,
      endPage:1
    };
  },
  created() {
    this.fetchData();
    console.log(this.count);
  },
  components: {
    SearchBar,
    MainHeader,
    LocationWrapper,
    FilterSetting,
    TrainerCard,
    NoResult,
    KakaoMap,
  },
  methods: {
    fetchData() {
      axios
        .get(
          `/api/hr2023/trainer/?page=` +
            this.pageNum +
            `&search=` +
            this.searchName,
          {
            headers: {
              Authorization:
                `Token ` + `9d8443df0dbd0864511362bcd7c8ea52daf7e481`,
            },
          }
        ) // 해당 url에서 제공하는 데이터를 가져옴.
        .then((response) => {
          console.log(response.data.count);
          this.count = response.data.count;
          if(this.count !== 0){
            this.results = response.data.results;
          }
          this.endPage = Math.floor(this.count / 10) + 1;
          console.log("endPage : ",this.endPage)
          console.log("pageNum : ",this.pageNum)

        })
        .catch(function (err) {
          console.log(err);
        });
    },
    changeOrderingMode(mode) {
      this.orderingMode = mode;
    },
    moveNextPage() {
      if (this.pageNum < this.endPage) {
        this.pageNum += 1;
        this.fetchData();
      } else {
        alert("마지막 페이지입니다.");
      }
    },
    movePreviousPage() {
      if (this.pageNum !== 1) {
        this.pageNum -= 1;
        this.fetchData();
      } else {
        alert("첫 페이지입니다.");
      }
    },
    setPageNum(pageNum) {
      this.pageNum = pageNum;
    },
    setSearchName(searchName) {
      this.searchName = searchName;
    },
    resetPageNum(){
      this.pageNum = 1;
    }
  },
};
</script>

<style lang="scss" scoped>
#app {
  display: flex;
  flex-direction: column;
  max-width: 100vw;
  min-width: 100vw;
  max-height: 100vh;
  min-height: 100vh;
  *{
    background: #ffffff;
    font-family: "Pretendard";
    font-style: normal;
    font-weight: 400;
    background: #ffffff;
  }

}
.fade-enter-active,
.fade-leave-active {
  position: absolute;
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
#content {
  position: relative;
  min-width: 100%;
  flex: 1;
  #kMap {
    position: absolute;
    min-height: 100vh;

    top: 0;
    left: 0;
    z-index: 0;
  }
  #sideBar {
    position: absolute;
    flex: 1;
    top: 0;
    left: 0;
    z-index: 1;
    display: flex;
    flex-direction: column;

    #fadeWrapper {
      flex: 1;
      max-height: 100vh;
      overflow-y: scroll;
      &::-webkit-scrollbar {
        // hide scrollBar
        display: none;
      }
    }
  }
}
#gotoPageContainer {
  display: flex;
  width: 480px;
  height: 100px;
  align-items: center;
  justify-content: space-between;
  padding: 0px 24px;

  > div {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 40px;
    border-radius: 24px;
  }
}
</style>
