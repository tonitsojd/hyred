<template>
  <div id="app" class="page-shell">
    <aside class="left-rail">
      <img
        class="left-placeholder"
        src="./assets/images/sidebar_placeholder.png"
        alt="Sidebar placeholder"
      >
    </aside>

    <main class="content-stage">
      <section class="white-column">
        <div class="inner-pad">
          <div class="column-stack">
            <NewVideoHeader />
            <RecommendedPackageCard @open-info="openInfoOverlay" @open-edit="openEditOverlay" />
            <CreatorsCard @open-info="openInfoOverlay" />
            <CheckoutCard />
          </div>
        </div>
      </section>
    </main>

    <aside class="right-rail">
      <img
        class="right-placeholder"
        src="./assets/images/hooks_placeholder.png"
        alt="Hooks placeholder"
      >
    </aside>

    <div
      v-if="activeOverlay"
      class="faq-overlay"
      @click.self="closeActiveOverlay"
    >
      <div v-if="activeOverlay === 'faq'" class="faq-overlay__panel">
        <div class="faq-overlay__body">
          <FaqArticle :initial-section="infoOverlaySection" @close="closeActiveOverlay" />
        </div>
      </div>

      <div v-else-if="activeOverlay === 'edit'" class="customize-overlay__panel">
        <CustomizeVideoPopup @close="closeActiveOverlay" />
      </div>
    </div>
  </div>
</template>

<script>
import NewVideoHeader from './components/NewVideoHeader.vue'
import RecommendedPackageCard from './components/RecommendedPackageCard.vue'
import CreatorsCard from './components/CreatorsCard.vue'
import CheckoutCard from './components/CheckoutCard.vue'
import FaqArticle from './components/FaqArticle.vue'
import CustomizeVideoPopup from './components/CustomizeVideoPopup.vue'

export default {
  name: 'App',
  components: {
    NewVideoHeader,
    RecommendedPackageCard,
    CreatorsCard,
    CheckoutCard,
    FaqArticle,
    CustomizeVideoPopup,
  },
  data() {
    return {
      activeOverlay: null,
      infoOverlaySection: 'duration',
    }
  },
  watch: {
    activeOverlay(nextValue) {
      document.body.style.overflow = nextValue ? 'hidden' : ''
    },
  },
  methods: {
    openInfoOverlay(section = 'duration') {
      this.infoOverlaySection = section
      this.activeOverlay = 'faq'
    },
    openEditOverlay() {
      this.activeOverlay = 'edit'
    },
    closeActiveOverlay() {
      this.activeOverlay = null
    },
    handleEscape(event) {
      if (event.key === 'Escape' && this.activeOverlay) {
        this.closeActiveOverlay()
      }
    },
  },
  mounted() {
    window.addEventListener('keydown', this.handleEscape)
  },
  beforeDestroy() {
    document.body.style.overflow = ''
    window.removeEventListener('keydown', this.handleEscape)
  },
}
</script>

<style>
.page-shell {
  height: 100vh;
  display: grid;
  grid-template-columns: clamp(120px, 14vw, 260px) minmax(620px, 760px) minmax(520px, 860px);
  justify-content: center;
  overflow: hidden;
  background: var(--color-app-bg);
}

.left-rail {
  width: 100%;
  background: var(--color-app-bg);
  position: relative;
  overflow: hidden;
}

.left-placeholder {
  display: block;
  width: calc(100% - 32px);
  margin: 16px;
  position: sticky;
  top: 16px;
}

.content-stage {
  width: 100%;
  height: 100vh;
  overflow-y: auto;
  overflow-x: hidden;
  background: var(--color-surface);
  scroll-behavior: smooth;

  -ms-overflow-style: none;
  scrollbar-width: none;
}

.content-stage::-webkit-scrollbar {
  display: none;
}

.white-column {
  width: 100%;
  min-height: 100%;
  background: var(--color-surface);
}

.inner-pad {
  padding: 80px;
}

.column-stack {
  display: flex;
  flex-direction: column;
  gap: 40px;
  padding-bottom: 80px;
}

.right-rail {
  width: 100%;
  min-width: 0;
  background: #f5f5f5;
  position: relative;
  overflow: hidden;
  display: flex;
  justify-content: center;
}

.right-placeholder {
  display: block;
  width: 592px;
  height: 570px;
  max-width: none;
  flex: 0 0 auto;
  object-fit: contain;
  margin-top: 80px;
  position: sticky;
  top: 80px;
}

.faq-overlay {
  position: fixed;
  inset: 0;
  z-index: 20;
  display: flex;
  align-items: stretch;
  justify-content: center;
  padding: 24px;
  background: rgba(23, 23, 28, 0.44);
  backdrop-filter: blur(10px);
}

.faq-overlay__panel {
  position: relative;
  width: min(1240px, 100%);
  height: 100%;
  border-radius: 28px;
  background: rgba(255, 255, 255, 0.96);
  box-shadow: 0 32px 90px rgba(12, 17, 24, 0.18);
  overflow: hidden;
}

.faq-overlay__body {
  height: 100%;
  overflow-y: auto;
  overflow-x: hidden;
  padding: 0;
  scroll-behavior: smooth;
}

.faq-overlay__body::-webkit-scrollbar {
  width: 10px;
}

.faq-overlay__body::-webkit-scrollbar-thumb {
  background: rgba(26, 26, 26, 0.16);
  border-radius: 999px;
}

.customize-overlay__panel {
  width: 556px;
  max-width: calc(100vw - 32px);
  margin: auto;
  max-height: 100%;
  overflow-y: auto;
  overflow-x: hidden;
  -webkit-overflow-scrolling: touch;
}

@media (max-width: 1400px) {
  .page-shell {
    grid-template-columns: clamp(120px, 13vw, 220px) minmax(560px, 700px) minmax(420px, 700px);
  }
}

@media (max-width: 1200px) {
  .page-shell {
    grid-template-columns: 104px minmax(500px, 620px) minmax(340px, 500px);
  }

  .left-placeholder {
    width: calc(100% - 16px);
    margin: 8px;
    top: 8px;
  }

  .right-placeholder {
    margin-top: 48px;
    top: 48px;
    width: 592px;
    height: 570px;
  }

  .faq-overlay__body {
    padding: 0 48px 56px;
  }
}

@media (max-width: 900px) {
  html,
  body,
  #app {
    height: auto;
  }

  body {
    overflow: auto;
  }

  .page-shell {
    display: block;
    height: auto;
    overflow: visible;
    background: #ffffff;
  }

  .left-rail,
  .right-rail {
    display: none;
  }

  .white-column {
    width: 100%;
    min-height: auto;
  }

  .inner-pad {
    padding: 24px 14px 28px;
  }

  .column-stack {
    gap: 36px;
    padding-bottom: 20px;
  }

  .faq-overlay {
    padding: 0;
    background: rgba(23, 23, 28, 0.72);
  }

  .faq-overlay__panel {
    width: 100%;
    height: 100%;
    border-radius: 0;
  }

  .faq-overlay__close {
    top: 16px;
    right: 16px;
  }

  .faq-overlay__body {
    padding: 0;
  }

  .customize-overlay__panel {
    width: 100%;
    max-width: 100%;
    height: 100%;
    padding: 16px;
  }
}
</style>
