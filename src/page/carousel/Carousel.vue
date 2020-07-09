<template>
  <div class="slider">
    <div class="slides">
      <div class="slide">
        <img src="../../img/dog1.jpg" alt="" />
      </div>
      <div class="slide">
        <img src="../../img/dog2.jpg" alt="" />
      </div>
      <div class="slide">
        <img src="../../img/dog3.jpg" alt="" />
      </div>
      <div class="slide">
        <img src="../../img/dog4.jpg" alt="" />
      </div>
    </div>
    <div @click="prev" class="btn-left fas fa-chevron-left"></div>
    <div @click="next" class="btn-right fas fa-chevron-right"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      index: 0,
      carousel: null,
    };
  },
  methods: {
    prev() {
      let slides = $(".slide");
      if (this.index == 0) this.index = slides.length - 1;
      else this.index--;
      slides[0].style.marginLeft = "-" + this.index * 600 + "px";
    },
    next() {
      let slides = $(".slide");
      if (this.index == slides.length - 1) this.index = 0;
      else this.index++;
      slides[0].style.marginLeft = "-" + this.index * 600 + "px";
    },
    setCarousel() {
      this.carousel = setInterval(this.next, 3000);
    },
  },
  mounted() {
    this.setCarousel();
  },
  beforeDestroy() {
    clearInterval(this.carousel);
  },
};
</script>

<style lang="scss" scoped>
body {
  margin: 0;
  padding: 0;
  .slider {
    position: relative;
    width: 600px;
    height: 400px;
    overflow: hidden;
    margin: auto;
  }
  .slides {
    width: 2400px;
    display: flex;
    .slide {
      width: 600px;
      transition: 0.6s;
      img {
        width: 100%;
      }
    }
  }
  .btn-left,
  .btn-right {
    position: absolute;
    width: 60px;
    height: 200px;
    top: 0;
    font-size: 40px;
    line-height: 400px !important;
    text-align: center;
    cursor: pointer;
    transition: 0.3s;
  }
  .btn-left {
    left: 0;
  }
  .btn-right {
    right: 0;
  }
}
</style>
