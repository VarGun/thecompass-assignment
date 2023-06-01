<template>
  <div id="app">
    <MainHeader class="Header" :setOpenModal="setOpenModal" :openModal="openModal"/>
    <div id="content">
      <KakaoMap id="kMap" />
      <UserModal :setOpenModal="setOpenModal" v-show="openModal" id="UserModal"/>

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

                  :class="{ hover: pageNum !== 1 && hoverPrevious }"
                  @mouseover="hoverPrevious = pageNum !== 1"
                  @mouseleave="hoverPrevious = false"

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
                  :class="{ hover: pageNum < endPage && hoverNext }"
                  @mouseover="hoverNext = pageNum < endPage"
                  @mouseleave="hoverNext = false"

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
import UserModal from "@/components/UserModal.vue";
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
      endPage:1,
      hoverPrevious: false,
      hoverNext: false,
      openModal: false
    };
  },
  created() {
    this.fetchData();
  },
  components: {
    SearchBar,
    MainHeader,
    LocationWrapper,
    FilterSetting,
    TrainerCard,
    NoResult,
    KakaoMap,
    UserModal
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
        )
        .then((response) => {
          this.count = response.data.count;
          if(this.count !== 0){
            this.results = response.data.results;
          }
          this.endPage = Math.floor(this.count % 10 === 0 ? this.count / 10 : this.count / 10 + 1)

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
    },
    setOpenModal(){
      this.openModal = !this.openModal;
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

  * {
    background: #ffffff;
    font-family: "Pretendard";
    font-style: normal;
    font-weight: 400;
    background: #ffffff;
  }
}

//.fade-enter-active,
//.fade-leave-active {
//  position: absolute;
//  transition: opacity 0.5s;
//}
//.fade-enter,
//.fade-leave-to {
//  opacity: 0;
//}

#content {
  position: relative;
  min-width: 100%;
  flex: 1;
  #UserModal{
    position: absolute;
    top: -40px;
    right: 20px;
  }
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
    overflow: hidden;
    border-bottom-right-radius: 24px;
    border-bottom-left-radius: 24px;

    #fadeWrapper {
      flex: 1;
      max-height: 80vh;
      overflow-y: scroll;
      &::-webkit-scrollbar {
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
  #btnPrevious:hover{
    color: #ffffff !important;
    border: none !important;
    background: #ff8000;
  }
  #btnNext:hover{
    color: #ffffff !important;
    border: none !important;
    background: #ff8000;
  }

}
</style>
