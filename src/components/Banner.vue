<template>
  <div class="carousel">
    <div class="carousel-item">
      <div class="red"></div>
    </div>
    <div class="carousel-item">
      <div class="green"></div>
    </div>
    <div class="carousel-item">
      <div class="yellow"></div>
    </div>
    <div class="carousel-item">
      <div class="violet"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },

  mounted() {
    var slides = document.getElementsByClassName("carousel-item");
    var self = this;
    this.addActive(slides[0]);

    setInterval(function () {
      console.log("setInterval");
      for (var i = 0; i < slides.length; i++) {
        if (i + 1 == slides.length) {
          self.addActive(slides[0]);
          slides[0].style.zIndex = 100;
          setTimeout(self.removeActive, 350, slides[i]);
          break;
        }
        if (slides[i].classList.contains("active")) {
          slides[i].removeAttribute("style");
          setTimeout(self.removeActive, 350, slides[i]);
          self.addActive(slides[i + 1]);
          break;
        }
      }
    }, 5000);
  },
  methods: {
    removeActive(slide) {
      slide.classList.remove("active");
    },
    addActive(slide) {
      slide.classList.add("active");
    },
  },
};
</script>

<style scoped>
.carousel {
  position: relative;
  width: 100%;
  height: 55vh;
  overflow: hidden;
  background-color: #cdcdcd;
}

.carousel-item {
  position: absolute;
  width: 100%;
  height: 100%;
  border: 1px solid #2e2e2e;
  top: 0;
  left: 100%;
}

.active {
  left: 0;
  transition: all 0.3s ease-out;
}
div {
  height: 100%;
}
.red {
  /* background-color: red; */
  background: url("https://media.istockphoto.com/photos/mountain-landscape-picture-id517188688?b=1&k=20&m=517188688&s=612x612&w=0&h=x8h70-SXuizg3dcqN4oVe9idppdt8FUVeBFemfaMU7w=");
  height: 100%;
  width: 100%;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.yellow {
  /* background-color: red; */
  background: url("https://images.unsplash.com/photo-1503023345310-bd7c1de61c7d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8aHVtYW58ZW58MHx8MHx8&w=1000&q=80");
  height: 100%;
  width: 100%;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
.green {
  background: url("https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885__480.jpg");
  height: 100%;
  width: 100%;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.violet {
  background: url("https://images.unsplash.com/photo-1541963463532-d68292c34b19?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8Mnx8fGVufDB8fHx8&w=1000&q=80");
  height: 100%;
  width: 100%;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
</style>