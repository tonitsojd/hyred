<template>
  <section class="faq-article">
    <header class="faq-header">
      <h2 class="faq-title">What we recommend and why</h2>
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
            <div class="hooks-table">
              <div class="hooks-table__head">
                <span class="hooks-table__head-spacer"></span>

                <div class="hooks-table__metrics-head">
                  <span>Spent</span>
                  <span>Impressions</span>
                  <span>Click-Through</span>
                  <span>Cost per result</span>
                </div>
              </div>

              <div
                v-for="hook in hooksRows"
                :key="hook.file"
                class="hooks-row"
                :class="{ 'is-featured': hook.featured }"
              >
                <div class="hooks-row__asset">
                  <img :src="hook.image" :alt="hook.file" class="hooks-row__thumb">
                  <span>{{ hook.file }}</span>
                </div>

                <div class="hooks-row__metrics">
                  <span>{{ hook.spent }}</span>
                  <span>{{ hook.impressions }}</span>
                  <span>{{ hook.ctr }}</span>
                  <span>{{ hook.cost }}</span>
                </div>
              </div>
            </div>

            <div class="hooks-note">
              <img :src="metaIllustration" alt="Meta result illustration" class="hooks-note__image">
              <span>– “good job”</span>
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
import META_ILLUSTRATION from '../assets/images/meta_guy.svg'
import EDITING_IMAGE from '../assets/images/3 Editing.png'
import CREATORS_IMAGE from '../assets/images/4 Creators.png'
import PHOTOS_IMAGE from '../assets/images/5 Photos.png'
import GUARANTEE_IMAGE from '../assets/images/6 Guarantee.png'

export default {
  name: 'FaqArticle',
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
      hooksRows: [
        {
          file: 'hook_1.mp4',
          image: 'https://www.figma.com/api/mcp/asset/c326aba6-f87d-4674-b125-0a916539e9f3',
          spent: '$18',
          impressions: '1,150',
          ctr: '0.8%',
          cost: '$18.00',
          featured: false,
        },
        {
          file: 'hook_2.mp4',
          image: 'https://www.figma.com/api/mcp/asset/5c31a9e3-9466-4303-a440-8995f2615666',
          spent: '$41',
          impressions: '2,050',
          ctr: '1.4%',
          cost: '$10.20',
          featured: false,
        },
        {
          file: 'hook_3.mp4',
          image: 'https://www.figma.com/api/mcp/asset/47c85680-8fab-4c9a-a376-537873a5001d',
          spent: '$87',
          impressions: '4,400',
          ctr: '2.6%',
          cost: '$6.40',
          featured: true,
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
      metaIllustration: META_ILLUSTRATION,
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
  z-index: 3;
  margin: 0 -56px 28px;
  padding: 32px 120px 24px 56px;
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

.faq-grid {
  display: grid;
  grid-template-columns: 154px 726px;
  column-gap: 100px;
  align-items: start;
  margin-top: 40px;
}

.faq-nav {
  position: sticky;
  top: 96px;
  z-index: 2;
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-self: start;
  padding: 4px 0 8px;
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

.hooks-table {
  width: 726px;
  border-radius: 18px;
  overflow: hidden;
  background: #e2eee1;
}

.hooks-table__head,
.hooks-row {
  display: grid;
  grid-template-columns: 313px 413px;
  align-items: center;
}

.hooks-table__head {
  min-height: 44px;
  background: rgba(226, 238, 225, 0.94);
}

.hooks-table__head-spacer {
  display: block;
}

.hooks-table__metrics-head,
.hooks-row__metrics {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  align-items: center;
  transform: translateX(-64px);
}

.hooks-table__metrics-head span {
  font-weight: var(--font-weight-medium);
  font-size: 10px;
  line-height: 1;
  text-align: center;
  color: var(--faq-body-color);
}

.hooks-row {
  min-height: 74px;
}

.hooks-row.is-featured {
  background: #9fea68;
}

.hooks-row__asset {
  display: flex;
  align-items: center;
  gap: 24px;
  padding: 0 18px;
}

.hooks-row__asset span {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1;
  letter-spacing: -0.02em;
  color: var(--faq-body-color);
}

.hooks-row.is-featured .hooks-row__asset span {
  font-weight: var(--font-weight-semibold);
  color: var(--color-text);
}

.hooks-row__thumb {
  width: 48px;
  height: 48px;
  border-radius: 6px;
  object-fit: cover;
  display: block;
  flex: 0 0 auto;
}

.hooks-row__metrics span {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1;
  text-align: center;
  color: var(--faq-body-color);
}

.hooks-row.is-featured .hooks-row__metrics span {
  font-weight: var(--font-weight-semibold);
  color: var(--color-text);
}

.hooks-note {
  position: absolute;
  right: -138px;
  bottom: -4px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.hooks-note__image {
  width: 84px;
  height: auto;
  display: block;
}

.hooks-note span {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1;
  color: var(--faq-body-color);
  white-space: nowrap;
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
  .faq-title {
    font-size: 28px;
  }

  .faq-grid {
    grid-template-columns: 1fr;
    row-gap: 24px;
  }

  .faq-nav {
    position: sticky;
    top: 72px;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 10px 12px;
  }

  .faq-intro {
    grid-template-columns: 1fr;
    row-gap: 16px;
    width: 100%;
  }

  .faq-section-heading {
    width: 214px;
    max-width: 100%;
  }

  .faq-content,
  .faq-section,
  .duration-table,
  .faq-visual-panel {
    width: 100%;
    min-width: 0;
  }

  .faq-content {
    padding-bottom: 24vh;
  }

  .duration-table {
    grid-template-columns: 1fr;
  }

  .duration-card {
    min-height: 0;
  }

  .faq-section + .faq-section {
    margin-top: 72px;
  }

  .hooks-layout,
  .hooks-table {
    width: 100%;
  }

  .hooks-table__head {
    display: none;
  }

  .hooks-row {
    grid-template-columns: 1fr;
    min-height: 0;
    padding: 14px 16px;
    gap: 14px;
  }

  .hooks-row__asset {
    padding: 0;
    gap: 14px;
  }

  .hooks-row__metrics {
    gap: 10px;
  }

  .hooks-note {
    position: static;
    margin-top: 14px;
    justify-content: flex-end;
  }

  .process-list {
    width: 100%;
  }
}
</style>
