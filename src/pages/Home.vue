<script>
import Navbar from "../components/Navbar.vue";
import Footer from "../components/Footer.vue";
import ProductDisplay from "../components/Productdisplay.vue";
import Aboutme from "../components/Aboutme.vue";
import Fullscreenviewer from "../components/Fullscreenviewer.vue";
import GridCombined from "../components/GridCombined.vue";
import ScreenSizeWarningPopup from "../components/ScreenSizeWarningPopup.vue";
import { onMounted } from "vue";

export default {
  setup() {
    onMounted(() => {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add("show");
          }
        });
      });

      const hiddenElements = document.querySelectorAll(".hidden");

      if (hiddenElements) {
        hiddenElements.forEach((el) => observer.observe(el));
      }
    });
  },
  components: {
    Navbar,
    Footer,
    ProductDisplay,
    Aboutme,
    GridCombined,
    Fullscreenviewer,
    ScreenSizeWarningPopup,
  },
  data() {
    return {
      selectedImage: null,
      isFullViewerOpen: false,
    };
  },
  methods: {
    openFullViewer(image) {
      this.selectedImage = image;

      this.isFullViewerOpen = true;
    },
    closeFullViewer() {
      this.isFullViewerOpen = false;
    },
  },
};
</script>

<template>
  <nav>
    <Navbar class="hidden" />
  </nav>
  <ScreenSizeWarningPopup />
  <Fullscreenviewer
    v-if="isFullViewerOpen"
    :selectedImage="selectedImage"
    :type="type"
    @close="closeFullViewer"
  />
  <div class="innerbody">
    <main>
      <section class="Photos hidden">
        <GridCombined @open-fullviewer="openFullViewer" />
      </section>
    </main>
    <footer>
      <Footer class="hidden" />
    </footer>
  </div>
</template>

<style scoped>
/* Add component-specific styles here */
</style>
