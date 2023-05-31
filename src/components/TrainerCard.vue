<template>
  <div class="TrainerCard">
    <img src="../../public/Images/TrainerImg.svg" />
    <div class="TrainerInfo">
      <div class="featureContainer">
        <div class="onlyFemale" v-show="is_for_women">여성전문</div>
        <div class="onlyOne" v-show="is_serve_welcome">1회체험</div>
      </div>
      <div class="InfoContainer">
        <div class="nameContainer" id="textBold">{{ name }} 트레이너</div>
        <div class="gradeContainer">
          {{ score }}
          <div class="grades">
            <img
              v-for="i in score"
              :key="i"
              src="../../public/Images/StarFull.svg"
            />
            <img
              v-for="i in 5 - score"
              :key="i"
              src="../../public/Images/StarEmpty.svg"
            />
          </div>
          <div id="textGrey">({{ review }})</div>
        </div>
        <div class="trainerComment">
          {{ introduce }}
        </div>
        <div class="priceContainer">
          <div>
            <div id="textBigBold">63</div>
            <!--            <div id="textBigBold">{{ discount_rate }}</div>-->
            %
          </div>
          <div>
            <div id="textBigBold">{{ calc_price }}</div>
            원
          </div>
          <div>
            <div>{{ price }}원</div>
          </div>
        </div>
        <div class="trainerLocation">
          <img src="../../public/Images/LocationGrey.svg" />
          <div>{{ place }} · 논현역 도보 1분</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TrainerCard",
  props: [`trainers`],
  data() {
    return {
      name: "",
      score: 0,
      place: "",
      review: 0,
      is_for_women: false,
      is_serve_welcome: false,
      introduce: "",
      price: 0,
      calc_price: 0,
      discount_rate: 0,
    };
  },
  created() {
    this.setData();
  },
  methods: {
    setData() {
      this.name = this.trainers.name;
      this.score = this.trainers.score;
      this.place = this.trainers.place;
      this.review = this.trainers.review;
      this.is_for_women = this.trainers.is_for_women;
      this.is_serve_welcome = this.trainers.is_serve_welcome;
      this.introduce = this.trainers.introduce;
      this.price = this.trainers.price;
      this.calc_price = this.trainers.calc_price;
      // this.discount_rate =
      //   100 - (this.trainers.calc_price / this.trainers.price) * 100;
    },
  },
};
</script>

<style scoped lang="scss">
.TrainerCard {
  display: flex;
  width: 480px;
  padding: 16px;
  gap: 16px;
}

// font style
#textBold {
  font-weight: 700;
}
#textBigBold {
  font-weight: 700;
  font-size: 18px;
}
#textGrey {
  color: #98a5b3;
}

.TrainerInfo {
  flex: 1;
  height: 160px;
  position: relative;
  font-size: 16px;
  .featureContainer {
    position: absolute;
    right: 0;
    display: flex;
    align-items: center;
    gap: 4px;
    > div {
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 12px;
      font-weight: 500;
      width: 58px;
      height: 24px;
      border-radius: 16px;
    }
    .onlyFemale {
      color: #ff3377;
      background: #ff337708;
    }
    .onlyOne {
      color: #0080ff;
      background: #0080ff08;
    }
  }
  .InfoContainer {
    position: absolute;
    left: 0;
    top: 8px;
    display: flex;
    flex-direction: column;
    gap: 8px;
    > div {
      display: flex;
    }
    .gradeContainer {
      gap: 4px;
      align-items: center;
    }
    .trainerComment {
      font-size: 14px;
      color: #3d454d;
    }
    .priceContainer {
      gap: 8px;
      font-size: 12px;
      align-items: baseline;
      color: #ff8000;

      > div {
        display: flex;
        align-items: baseline;
      }
      div:nth-child(2) {
        color: #3d454d;
      }
      div:nth-child(3) {
        color: #6c7680;
        text-decoration-line: line-through;
      }
    }
    .trainerLocation {
      gap: 6px;
      font-size: 14px;
    }
  }
}
</style>
