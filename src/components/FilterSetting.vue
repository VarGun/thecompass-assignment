<template>
  <div class="FilterSetting">
    <div class="filterHeader">
      <img
        src="../../public/Images/ArrowLeft.svg"
        @click="changeOrderingMode"
      />
      <div class="textGrey">필터 초기화</div>
    </div>
    <hr class="underLine" />
    <div class="filteringContainer">
      <div class="textBold">정렬</div>
      <div class="radioContainer">
        <div class="checkContainer">
          <img src="../../public/Images/Checked.svg" />
          <div class="textOrange">추천순</div>
        </div>
        <div class="uncheckContainer">
          <img src="../../public/Images/Unchecked.svg" />
          <div>거리순</div>
        </div>
      </div>
    </div>
    <hr />
    <div class="rangeContainer">
      <div class="textContainer">
        <div class="textBold">검색 반경</div>
        <div class="textOrange">1km 이내</div>
      </div>
      <div class="barContainer">
        <div class="barBackground" />
        <div class="barRange">
          <div class="barThumb" />
        </div>
      </div>
      <div class="textGrey">500m</div>
    </div>
    <hr />
    <hr />
    <div class="selectGender">
      <div class="textBold">트레이너 성별</div>
      <div class="genderContainer">
        <div>
          <img src="../../public/Images/Checked.svg" />
          <div class="textOrange">전체</div>
        </div>
        <div>
          <img src="../../public/Images/Unchecked.svg" />
          <div>여</div>
        </div>
        <div>
          <img src="../../public/Images/Unchecked.svg" />
          <div>남</div>
        </div>
      </div>
    </div>
    <hr />
    <div class="onlyFemaleCheck">
      <div class="textBold">여성 전문</div>
      <img src="../../public/Images/UncheckedBox.svg" />
    </div>
    <hr />
    <hr />
    <div class="applyBtn">
      <div class="textBold">필터 적용하기</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FilterSetting",
  props: [`orderingMode`],
  methods: {
    changeOrderingMode() {
      this.$emit(`update-mode`, true);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.FilterSetting {
  width: 480px;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 16px;
  font-weight: 400;
  color: #3d454d;
  padding: 16px;
  gap: 16px;
  background: #ffffff;

  > hr {
    width: 448px;
    height: 0px;
    border: none;
  }
  .underLine {
    border: 1px solid #e4eaf0;
  }
  > div {
    width: 448px;
    height: 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
}
// font style
.textOrange {
  color: #ff8000;
}
.textBold {
  font-weight: 700;
}
.textGrey {
  color: #6c7680;
}

.filterHeader {
  color: #6c7680;
  margin-bottom: 16px;
}
.filteringContainer {
  font-weight: 700;
  .radioContainer {
    display: flex;
    align-items: center;
    gap: 26px;
    font-weight: 400;

    > div {
      display: flex;
      align-items: center;
      gap: 10px;
    }
  }
}

.rangeContainer {
  flex-direction: column;
  gap: 16px;
  > div {
    width: 100%;
  }
  .textContainer {
    display: flex;
    gap: 12px;
  }
  .barContainer {
    position: relative;
    height: 36px;
    > div {
      position: absolute;
      height: 4px;
      border-radius: 4px;
    }
    .barBackground {
      width: 100%;
      background: #e4eaf0;
      z-index: 1;
    }
    .barRange {
      width: 86px;
      background: #ff8000;
      z-index: 2;
      .barThumb {
        position: absolute;
        width: 12px;
        height: 12px;
        right: -4px;
        top: -4px;
        background: #ff8000;
        border-radius: 12px;
        z-index: 3;
      }
    }
  }
}
.genderContainer {
  display: flex;
  align-items: center;
  gap: 26px;
  > div {
    display: flex;
    align-items: center;
    gap: 10px;
  }
}
.applyBtn {
  border-radius: 6px;
  background: #ff8000;

  justify-content: center !important;
  height: 48px !important;
  > div {
    color: #ffffff;
  }
}
</style>
