<template>
  <section class="faq-article">
    <header class="faq-header">
      <h2 class="faq-title">What we recommend and why</h2>
      <button
        type="button"
        class="faq-header__close icon-button-reset interactive-hover"
        aria-label="Close article"
        @click="$emit('close')"
      >
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" aria-hidden="true">
          <path d="M4 4L20 20" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
          <path d="M20 4L4 20" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
        </svg>
      </button>
    </header>

    <div class="faq-grid">
      <nav class="faq-nav" aria-label="Article sections">
        <button
          v-for="section in sections"
          :key="section.id"
          type="button"
          class="faq-nav-link icon-button-reset"
          :class="{ 'is-active': section.id === activeSection }"
          @click="scrollToSection(section.id)"
        >
          {{ section.label }}
        </button>
      </nav>

      <div class="faq-content">
        <section id="faq-duration" class="faq-section faq-section--duration">
          <div class="faq-intro faq-intro--duration">
            <h3 class="faq-section-heading">balanced duration<br>for optimal start</h3>

            <div class="faq-copy-stack">
              <p class="faq-copy">15s is best for impulse purchases.<br>60s is for premium and complex products.</p>
              <p class="faq-copy">If you aren’t ready to commit to the extremes –<br>30s lets you do anything in between, get sales, and learn.</p>
            </div>
          </div>

          <div class="duration-table">
            <article
              v-for="option in durationOptions"
              :key="option.label"
              class="duration-card"
              :class="{ 'is-featured': option.featured }"
            >
              <h3 class="duration-card__title">{{ option.label }}</h3>
              <p class="duration-card__copy">{{ option.format }}</p>
              <p class="duration-card__copy">{{ option.platform }}</p>
            </article>
          </div>
        </section>

        <section id="faq-hooks" class="faq-section faq-section--hooks">
          <div class="faq-intro">
            <h3 class="faq-section-heading">intro is crucial,<br>but you never know<br>which is the best one</h3>

            <div class="faq-copy-stack">
              <p class="faq-copy">Good news: each hook is only 3 seconds.<br>It’s really inexpensive to make 3-5 of them.</p>
              <p class="faq-copy">Meta Ads Manager will find the winner automatically.<br>More hooks = better campaign performance on average.</p>
            </div>
          </div>

          <div class="hooks-layout">
            <div class="hooks-table-scroll">
              <img :src="hooksTableDesktopImage" alt="Hooks performance table" class="hooks-table-image hooks-table-image--desktop">
              <img :src="hooksTableMobileImage" alt="Hooks performance table" class="hooks-table-image hooks-table-image--mobile">
            </div>
          </div>
        </section>

        <section id="faq-editing" class="faq-section faq-section--editing">
          <div class="faq-intro">
            <h3 class="faq-section-heading">you probably don’t<br>have an editing team.<br>we do.</h3>

            <div class="faq-copy-stack">
              <p class="faq-copy">It costs us much less to edit a high quality final video,<br>than it will cost to you.</p>
              <p class="faq-copy">You will either have to spend more time, or more money<br>hiring someone. We will edit any video for €79.</p>
            </div>
          </div>

          <div class="faq-visual-panel">
            <img :src="editingImage" alt="Editing workflow illustration" class="faq-visual faq-visual--editing">
          </div>
        </section>

        <section id="faq-creators" class="faq-section faq-section--creators">
          <div class="faq-intro">
            <h3 class="faq-section-heading">the best creators apply<br>when they see the<br>money</h3>

            <div class="faq-copy-stack">
              <p class="faq-copy">We return 100% at any moment before you have confirmed your creators.<br>Choose how many creators you can afford at this time.</p>
              <p class="faq-copy">We don’t want to take money from you this early, but this policy<br>allows us to attract the best creators in the world.</p>
              <p class="faq-copy">Book 4 creators or more, and get one for free.</p>
            </div>
          </div>

          <div class="faq-visual-panel">
            <img :src="creatorsImage" alt="Creators collage" class="faq-visual faq-visual--creators">
          </div>
        </section>

        <section id="faq-photos" class="faq-section faq-section--photos">
          <div class="faq-intro">
            <h3 class="faq-section-heading">photos for your<br>campaign</h3>

            <div class="faq-copy-stack">
              <p class="faq-copy">Visual campaign continuity improves sales.</p>
              <p class="faq-copy">Ads, emails, organic social media posts -<br>everything works better with real matching photos.</p>
            </div>
          </div>

          <div class="faq-visual-panel">
            <img :src="photosImage" alt="Photo campaign examples" class="faq-visual faq-visual--photos">
          </div>
        </section>

        <section id="faq-guarantee" class="faq-section faq-section--guarantee">
          <div class="faq-intro">
            <h3 class="faq-section-heading">performance guarantee</h3>

            <div class="faq-copy-stack">
              <p class="faq-copy">We issue full refund, if Hyred videos underperform your current ads.</p>
              <p class="faq-copy">Performance Guarantee is included when<br>you book 3 creators or more.</p>
            </div>
          </div>

          <div class="faq-visual-panel">
            <img :src="guaranteeImage" alt="Performance guarantee illustration" class="faq-visual faq-visual--guarantee">
          </div>
        </section>

        <section id="faq-the-process" class="faq-section faq-section--process">
          <div class="faq-intro faq-intro--process">
            <h3 class="faq-section-heading">how we work<br>step by step</h3>

            <div class="process-list">
              <article
                v-for="step in processSteps"
                :key="step.title"
                class="process-item"
              >
                <h4 class="process-item__title">{{ step.title }}</h4>
                <p class="process-item__copy">{{ step.copy }}</p>
              </article>
            </div>
          </div>
        </section>
      </div>
    </div>
  </section>
</template>

<script>
import EDITING_IMAGE from '../assets/images/3 Editing.png'
import CREATORS_IMAGE from '../assets/images/4 Creators.png'
import PHOTOS_IMAGE from '../assets/images/5 Photos.png'
import GUARANTEE_IMAGE from '../assets/images/6 Guarantee.png'
import HOOKS_TABLE_DESKTOP_IMAGE from '../assets/icons/test_hooks_table_desktop.svg'
import HOOKS_TABLE_MOBILE_IMAGE from '../assets/icons/test_hooks_table.svg'

export default {
  name: 'FaqArticle',
  emits: ['close'],
  props: {
    initialSection: {
      type: String,
      default: 'duration',
    },
  },
  data() {
    return {
      activeSection: 'duration',
      observer: null,
      isProgrammaticScroll: false,
      scrollSettleTimeout: null,
      sections: [
        { id: 'duration', label: 'Duration' },
        { id: 'hooks', label: 'Hooks' },
        { id: 'editing', label: 'Editing' },
        { id: 'creators', label: 'Creators' },
        { id: 'photos', label: 'Photos' },
        { id: 'guarantee', label: 'Guarantee' },
        { id: 'the-process', label: 'The Process' },
      ],
      durationOptions: [
        {
          label: '15s.',
          format: 'Quick message, unboxing, fashion & accessories.',
          platform: 'TikTok, Instagram Reels, YouTube Shorts.',
          featured: false,
        },
        {
          label: '30s.',
          format: 'Full story: problem, solution (your product), call to action.',
          platform: 'Standard for Facebook & Instagram Ads.',
          featured: true,
        },
        {
          label: '60s.',
          format: 'Complex products, tutorials, storytelling.',
          platform: 'Website content, organic socials or retargeting.',
          featured: false,
        },
      ],
      processSteps: [
        {
          title: 'Create the order',
          copy: 'We hold your payment until the creator has delivered.',
        },
        {
          title: 'Generate the brief',
          copy: 'Share your product, and we’ll create the script in minutes.',
        },
        {
          title: 'Pick your favourite creator',
          copy: 'Creators apply for your assignment. You view their portfolio and choose who you want to work with.',
        },
        {
          title: 'Approve the video',
          copy: 'Creators deliver the first draft video content. Unlimited revisions within the scope of the brief.',
        },
        {
          title: 'The video is yours forever',
          copy: 'The full rights are transferred to you automatically upon approval.',
        },
      ],
      hooksTableDesktopImage: HOOKS_TABLE_DESKTOP_IMAGE,
      hooksTableMobileImage: HOOKS_TABLE_MOBILE_IMAGE,
      editingImage: EDITING_IMAGE,
      creatorsImage: CREATORS_IMAGE,
      photosImage: PHOTOS_IMAGE,
      guaranteeImage: GUARANTEE_IMAGE,
    }
  },
  mounted() {
    this.activeSection = this.sections.some(section => section.id === this.initialSection)
      ? this.initialSection
      : 'duration'

    this.$nextTick(() => {
      this.setupObserver()
      this.scrollToSection(this.activeSection, false)
    })
  },
  beforeDestroy() {
    if (this.observer) {
      this.observer.disconnect()
    }

    if (this.scrollSettleTimeout) {
      window.clearTimeout(this.scrollSettleTimeout)
    }
  },
  watch: {
    initialSection(nextSection) {
      if (this.sections.some(section => section.id === nextSection)) {
        this.activeSection = nextSection
        this.$nextTick(() => {
          this.scrollToSection(nextSection, false)
        })
      }
    },
  },
  methods: {
    scrollToSection(sectionId, smooth = true) {
      const root = this.$el.closest('.faq-overlay__body')
      const target = this.$el.querySelector(`#faq-${sectionId}`)

      if (!root || !target) {
        return
      }

      this.activeSection = sectionId
      this.isProgrammaticScroll = true

      if (this.scrollSettleTimeout) {
        window.clearTimeout(this.scrollSettleTimeout)
      }

      const rootRect = root.getBoundingClientRect()
      const targetRect = target.getBoundingClientRect()
      const targetTopWithinRoot = targetRect.top - rootRect.top + root.scrollTop
      const centeredTargetScrollTop = targetTopWithinRoot - (root.clientHeight - target.offsetHeight) / 2
      const maxScrollTop = root.scrollHeight - root.clientHeight
      const nextScrollTop = Math.max(0, Math.min(centeredTargetScrollTop, maxScrollTop))

      root.scrollTo({
        top: nextScrollTop,
        behavior: smooth ? 'smooth' : 'auto',
      })

      this.scrollSettleTimeout = window.setTimeout(() => {
        this.isProgrammaticScroll = false
      }, smooth ? 800 : 0)
    },
    setupObserver() {
      const root = this.$el.closest('.faq-overlay__body')
      const sectionNodes = this.$el.querySelectorAll('.faq-section[id]')

      if (!root || !sectionNodes.length) {
        return
      }

      this.observer = new IntersectionObserver(
        entries => {
          if (this.isProgrammaticScroll) {
            return
          }

          const visibleEntries = entries
            .filter(entry => entry.isIntersecting)
            .sort((a, b) => b.intersectionRatio - a.intersectionRatio)

          if (visibleEntries.length) {
            this.activeSection = visibleEntries[0].target.id.replace('faq-', '')
          }
        },
        {
          root,
          rootMargin: '-28% 0px -28% 0px',
          threshold: [0.1, 0.25, 0.45, 0.65],
        }
      )

      sectionNodes.forEach(sectionNode => {
        this.observer.observe(sectionNode)
      })
    },
  },
}
</script>

<style scoped>
.faq-article {
  --faq-body-color: rgba(26, 26, 26, 0.65);

  padding-top: 0;
}

.faq-header {
  position: sticky;
  top: 0;
  z-index: 5;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
  margin: 0;
  padding: 32px 56px 24px;
  background: rgba(255, 255, 255, 0.98);
  border-bottom: 1px solid rgba(22, 22, 26, 0.16);
  backdrop-filter: blur(8px);
}

.faq-title {
  margin: 0;
  font-weight: var(--font-weight-semibold);
  font-size: 32px;
  line-height: 1;
  letter-spacing: -0.04em;
  color: var(--color-text);
}

.faq-header__close {
  flex: 0 0 auto;
  width: 40px;
  height: 40px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text);
  border-radius: 8px;
}

.faq-grid {
  display: grid;
  grid-template-columns: 154px 726px;
  column-gap: 100px;
  align-items: start;
  margin-top: 40px;
  padding-left: 32px;
}

.faq-nav {
  position: sticky;
  top: 96px;
  z-index: 4;
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-self: start;
  padding: 4px 0 8px;
  background: transparent;
}

.faq-nav-link {
  width: fit-content;
  padding: 12px;
  border-radius: 8px;
  font-weight: var(--font-weight-medium);
  font-size: 18px;
  line-height: 1.2;
  letter-spacing: -0.025em;
  color: var(--faq-body-color);
  text-decoration: none;
  background: transparent;
  cursor: pointer;
  transition: background-color 160ms ease, color 160ms ease;
}

.faq-nav-link:hover,
.faq-nav-link:focus-visible {
  background: rgba(226, 238, 225, 0.68);
  color: rgba(26, 26, 26, 0.9);
}

.faq-nav-link.is-active {
  background: #e2eee1;
  font-weight: var(--font-weight-semibold);
  color: var(--color-text);
}

.faq-content {
  width: 726px;
  min-width: 726px;
  padding-bottom: 42vh;
}

.faq-section {
  margin: 0;
  width: 726px;
}

.faq-section + .faq-section {
  margin-top: 120px;
}

.faq-intro {
  display: grid;
  grid-template-columns: 214px 488px;
  column-gap: 24px;
  align-items: start;
  width: 726px;
}

.faq-section-heading {
  width: 214px;
  margin: 0;
  font-weight: var(--font-weight-semibold);
  font-size: 18px;
  line-height: 1.22;
  letter-spacing: -0.03em;
  color: var(--color-text);
}

.faq-copy-stack {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.faq-copy {
  margin: 0;
  max-width: 488px;
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.28;
  letter-spacing: var(--letter-spacing-body);
  color: var(--faq-body-color);
}

.duration-table {
  margin-top: 28px;
  display: grid;
  grid-template-columns: 238px 250px 238px;
  border-radius: 18px;
  overflow: hidden;
  width: 726px;
}

.duration-card {
  min-height: 172px;
  padding: 18px 20px 16px;
  background: #e2eee1;
}

.duration-card.is-featured {
  background: #9fea68;
}

.duration-card__title {
  margin: 0 0 22px;
  font-weight: var(--font-weight-semibold);
  font-size: 18px;
  line-height: 1;
  letter-spacing: -0.02em;
  color: var(--color-text);
}

.duration-card__copy {
  margin: 0;
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.35;
  letter-spacing: var(--letter-spacing-body);
  color: var(--faq-body-color);
}

.duration-card__copy + .duration-card__copy {
  margin-top: 22px;
}

.hooks-layout {
  position: relative;
  width: 726px;
  margin-top: 28px;
}

.hooks-table-scroll {
  width: 726px;
}

.hooks-table-image {
  display: block;
  width: 726px;
  height: auto;
  border-radius: 18px;
}

.hooks-table-image--mobile {
  display: none;
}

.faq-visual-panel {
  width: 726px;
  margin-top: 28px;
  border-radius: 18px;
  overflow: hidden;
  background: #e2eee1;
}

.faq-visual {
  display: block;
  width: 100%;
  height: auto;
}

.faq-visual--editing,
.faq-visual--creators,
.faq-visual--photos,
.faq-visual--guarantee {
  object-fit: cover;
}

.faq-intro--process {
  align-items: start;
}

.process-list {
  display: flex;
  flex-direction: column;
  gap: 32px;
  width: 488px;
}

.process-item__title {
  margin: 0 0 6px;
  font-weight: var(--font-weight-semibold);
  font-size: 16px;
  line-height: 1.2;
  letter-spacing: -0.02em;
  color: var(--color-text);
}

.process-item__copy {
  margin: 0;
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.35;
  letter-spacing: var(--letter-spacing-body);
  color: var(--faq-body-color);
}

@media (max-width: 900px) {
  .faq-header {
    margin: 0;
    padding: 10px 16px 14px;
    gap: 16px;
  }

  .faq-title {
    font-size: 24px;
    line-height: 1.06;
    letter-spacing: -0.04em;
  }

  .faq-header__close {
    width: 32px;
    height: 32px;
  }

  .faq-grid {
    display: block;
    margin-top: 0;
    padding-left: 0;
  }

  .faq-nav {
    position: sticky;
    top: 76px;
    z-index: 4;
    flex-direction: row;
    flex-wrap: nowrap;
    gap: 12px;
    width: 100%;
    margin: 0;
    padding: 14px 16px 16px;
    box-sizing: border-box;
    overflow-x: auto;
    overflow-y: hidden;
    white-space: nowrap;
    scrollbar-width: none;
    border-bottom: 1px solid rgba(22, 22, 26, 0.16);
    background: rgba(255, 255, 255, 0.98);
    backdrop-filter: blur(8px);
  }

  .faq-nav::-webkit-scrollbar {
    display: none;
  }

  .faq-nav-link {
    flex: 0 0 auto;
    font-size: 16px;
    line-height: 1.15;
    padding: 10px 14px;
  }

  .faq-intro {
    grid-template-columns: 1fr;
    row-gap: 14px;
    width: 100%;
  }

  .faq-section-heading {
    width: 214px;
    max-width: 100%;
    font-size: 14px;
    line-height: 1.16;
  }

  .faq-content,
  .faq-section,
  .duration-table,
  .faq-visual-panel,
  .hooks-layout,
  .hooks-table-scroll {
    width: 100%;
    min-width: 0;
  }

  .faq-content {
    padding: 20px 0 32vh;
  }

  .faq-copy-stack {
    gap: 12px;
  }

  .faq-copy {
    max-width: none;
    font-size: 14px;
    line-height: 1.24;
  }

  .duration-table {
    margin-top: 18px;
    grid-template-columns: 1fr;
    border-radius: 12px;
  }

  .duration-card {
    min-height: 0;
    padding: 12px 14px;
  }

  .duration-card__title {
    margin-bottom: 14px;
    font-size: 14px;
  }

  .duration-card__copy {
    font-size: 11px;
    line-height: 1.25;
  }

  .duration-card__copy + .duration-card__copy {
    margin-top: 14px;
  }

  .faq-section + .faq-section {
    margin-top: 80px;
  }

  .hooks-layout {
    margin-top: 18px;
  }

  .hooks-table-scroll {
    overflow-x: auto;
    overflow-y: visible;
    padding-bottom: 4px;
    scrollbar-width: none;
  }

  .hooks-table-scroll::-webkit-scrollbar {
    display: none;
  }

  .hooks-table-image--desktop {
    display: none;
  }

  .hooks-table-image--mobile {
    display: block;
    min-width: 538px;
    width: 538px;
    border-radius: 12px;
  }

  .process-list {
    width: 100%;
    gap: 24px;
  }

  .process-item__title {
    margin-bottom: 4px;
    font-size: 16px;
  }

  .process-item__copy {
    font-size: 14px;
    line-height: 1.24;
  }

  .faq-visual-panel {
    margin-top: 18px;
    border-radius: 12px;
  }
}
</style>
