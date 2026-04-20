<template>
  <section class="faq-article">
    <div class="faq-grid">
      <nav class="faq-nav" aria-label="Article sections">
        <a
          v-for="section in sections"
          :key="section.id"
          :href="`#faq-${section.id}`"
          class="faq-nav-link interactive-hover"
          :class="{ 'is-active': activeSection === section.id }"
          @click.prevent="scrollToSection(section.id)"
        >
          {{ section.label }}
        </a>
      </nav>

      <div class="faq-content">
        <h2 class="faq-title">What we recommend and why:</h2>

        <section id="faq-duration" class="faq-section faq-section--duration" data-anchor-section data-section-id="duration">
          <div class="faq-lead">
            <h3 class="faq-section-heading">balanced duration</h3>
            <p class="faq-copy">15s is best for impulse purchases.<br>60s is for premium and complex products.</p>
            <p class="faq-copy">If you aren’t ready to commit to the extremes - 30s lets you do just about anything in between, get sales, and learn.</p>
          </div>

          <div class="duration-table">
            <div class="duration-table__labels">
              <span>Duration</span>
              <span>Format</span>
              <span>Platform</span>
            </div>

            <div class="duration-table__columns">
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
          </div>
        </section>

        <section id="faq-hooks" class="faq-section" data-anchor-section data-section-id="hooks">
          <div class="faq-copy-stack">
            <h3 class="faq-section-heading">intro is the most important and unpredictable part of the video.</h3>
            <p class="faq-copy">Good news: short duration makes it really inexpensive to make 3-5 of them.</p>
            <p class="faq-copy">Meta Ads Manager will find the winner automatically.<br>More hooks = better campaign performance on average.</p>
          </div>

          <div class="hooks-panel">
            <div class="hooks-table">
              <div class="hooks-table__head">
                <span></span>
                <span>Spent</span>
                <span>Impressions</span>
                <span>Click-Through</span>
                <span>Cost per result</span>
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
                <span>{{ hook.spent }}</span>
                <span>{{ hook.impressions }}</span>
                <span>{{ hook.ctr }}</span>
                <span>{{ hook.cost }}</span>
              </div>
            </div>

            <div class="hooks-note">
              <img :src="metaIllustration" alt="Meta result illustration" class="hooks-note__image">
              <span>- "good job"</span>
            </div>
          </div>
        </section>

        <section id="faq-editing" class="faq-section" data-anchor-section data-section-id="editing">
          <div class="faq-copy-stack">
            <h3 class="faq-section-heading">you probably don’t have an editing team. we do.</h3>
            <p class="faq-copy">It costs us much less to edit a high quality final video,<br>than it will cost to you.</p>
            <p class="faq-copy">You will either have to spend more time, or more money hiring someone.<br>We will edit any video for €79.</p>
          </div>

          <img :src="editingImage" alt="Editing workflow illustration" class="faq-visual faq-visual--editing">
        </section>

        <section id="faq-creators" class="faq-section" data-anchor-section data-section-id="creators">
          <div class="faq-copy-stack faq-copy-stack--dense">
            <h3 class="faq-section-heading">the best creators apply when they see the money.</h3>
            <p class="faq-copy">We return 100% at any moment before you have confirmed your creators.<br>Choose how many creators you can afford at this time.</p>
            <p class="faq-copy">In the end you will receive one fully edited video, with multiple hooks, per creator.<br>We don’t want to take money from you this early, but this policy allows us to attract<br>the best creators in the world.</p>
            <p class="faq-copy">Book 4 creators or more, and get one for free.</p>
          </div>
        </section>

        <section id="faq-photos" class="faq-section" data-anchor-section data-section-id="photos">
          <div class="faq-copy-stack">
            <h3 class="faq-section-heading">visual campaign continuity improves sales.</h3>
            <p class="faq-copy">Ads, emails, organic social media posts - everything works better<br>with real matching photos.</p>
          </div>

          <img :src="photosImage" alt="Photo campaign examples" class="faq-visual faq-visual--photos">
        </section>

        <section id="faq-guarantee" class="faq-section" data-anchor-section data-section-id="guarantee">
          <div class="faq-copy-stack">
            <h3 class="faq-section-heading">We will refund you 50%, if Hyred videos underperform your current ads.</h3>
            <p class="faq-copy">Performance Guarantee is included when you book 3 creators or more.</p>
          </div>
        </section>

        <section id="faq-the-process" class="faq-section faq-section--process" data-anchor-section data-section-id="the-process">
          <div class="faq-process-tag">the process</div>

          <div class="faq-process-list">
            <article
              v-for="step in processSteps"
              :key="step.title"
              class="faq-process-item"
            >
              <h3 class="faq-process-item__title">{{ step.title }}</h3>
              <p class="faq-process-item__copy">{{ step.copy }}</p>
            </article>
          </div>
        </section>
      </div>
    </div>
  </section>
</template>

<script>
const HOOK_THUMB_1 = 'https://www.figma.com/api/mcp/asset/c326aba6-f87d-4674-b125-0a916539e9f3'
const HOOK_THUMB_2 = 'https://www.figma.com/api/mcp/asset/5c31a9e3-9466-4303-a440-8995f2615666'
const HOOK_THUMB_3 = 'https://www.figma.com/api/mcp/asset/47c85680-8fab-4c9a-a376-537873a5001d'
const EDITING_IMAGE = 'https://www.figma.com/api/mcp/asset/b4028edb-d51a-4816-a80f-a1c6c0cfe45d'
const PHOTOS_IMAGE = 'https://www.figma.com/api/mcp/asset/0d8f697a-0988-42d9-9580-71df2ce08cf4'
const META_ILLUSTRATION = 'https://www.figma.com/api/mcp/asset/1d51988f-c1dd-44f2-9e91-41f728cdaa34'

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
          image: HOOK_THUMB_1,
          spent: '$18',
          impressions: '1,150',
          ctr: '0.8%',
          cost: '$18.00',
          featured: false,
        },
        {
          file: 'hook_2.mp4',
          image: HOOK_THUMB_2,
          spent: '$41',
          impressions: '2,050',
          ctr: '1.4%',
          cost: '$10.20',
          featured: false,
        },
        {
          file: 'hook_3.mp4',
          image: HOOK_THUMB_3,
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
          copy: 'Tell us what is your product, and we’ll create the script in minutes.',
        },
        {
          title: 'Pick a favourite creator',
          copy: 'Creators apply for your assignment. You view their portfolio and choose who you want to work with.',
        },
        {
          title: 'Review',
          copy: 'Creators have have 5 days to deliver the content. Unlimited revisions within the scope of the brief.',
        },
        {
          title: 'The video is yours forever',
          copy: 'Once you’ve approved, the full rights are transferred to you.',
        },
      ],
      editingImage: EDITING_IMAGE,
      photosImage: PHOTOS_IMAGE,
      metaIllustration: META_ILLUSTRATION,
    }
  },
  mounted() {
    this.activeSection = this.initialSection
    this.$nextTick(() => {
      this.setupObserver()
      this.scrollToSection(this.initialSection, false)
    })
  },
  watch: {
    initialSection(nextSection) {
      this.activeSection = nextSection
      this.$nextTick(() => {
        this.scrollToSection(nextSection, false)
      })
    },
  },
  beforeDestroy() {
    if (this.observer) {
      this.observer.disconnect()
    }
  },
  methods: {
    scrollToSection(sectionId, smooth = true) {
      const target = this.$el.querySelector(`#faq-${sectionId}`)
      if (target) {
        target.scrollIntoView({ behavior: smooth ? 'smooth' : 'auto', block: 'start' })
      }
    },
    setupObserver() {
      const root = this.$el.closest('.faq-overlay__body') || null
      const sections = this.$el.querySelectorAll('[data-anchor-section]')

      if (!root || !sections.length) {
        return
      }

      this.observer = new IntersectionObserver(
        entries => {
          const visibleEntries = entries
            .filter(entry => entry.isIntersecting)
            .sort((a, b) => b.intersectionRatio - a.intersectionRatio)

          if (visibleEntries.length) {
            this.activeSection = visibleEntries[0].target.dataset.sectionId
          }
        },
        {
          root,
          rootMargin: '-18% 0px -58% 0px',
          threshold: [0.2, 0.35, 0.5, 0.7],
        }
      )

      sections.forEach(section => {
        this.observer.observe(section)
      })
    },
  },
}
</script>

<style scoped>
.faq-article {
  padding-top: 72px;
}

.faq-grid {
  display: grid;
  grid-template-columns: 132px minmax(0, 1fr);
  column-gap: 46px;
  align-items: start;
}

.faq-nav {
  position: sticky;
  top: 80px;
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.faq-nav-link {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.2;
  letter-spacing: var(--letter-spacing-body);
  color: rgba(26, 26, 26, 0.5);
  text-decoration: none;
  transition: color 160ms ease, transform 160ms ease, opacity 160ms ease;
}

.faq-nav-link::after {
  content: '';
  display: inline-block;
  width: 0;
}

.faq-nav-link.is-active {
  font-weight: var(--font-weight-medium);
  color: var(--color-text);
  transform: none;
}

.faq-nav-link.is-active::before {
  content: '– ';
}

.faq-content {
  min-width: 0;
}

.faq-title {
  margin: 0 0 84px;
  font-weight: var(--font-weight-semibold);
  font-size: 20px;
  line-height: 1;
  letter-spacing: -0.025em;
  color: var(--color-text);
}

.faq-section {
  scroll-margin-top: 72px;
  margin-bottom: 104px;
}

.faq-section:last-child {
  margin-bottom: 0;
}

.faq-lead,
.faq-copy-stack {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.faq-copy-stack--dense {
  gap: 14px;
}

.faq-section-heading {
  margin: 0;
  max-width: 670px;
  font-weight: var(--font-weight-medium);
  font-size: 18px;
  line-height: 1.2;
  letter-spacing: -0.005em;
  color: var(--color-text);
}

.faq-copy {
  margin: 0;
  max-width: 670px;
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.2;
  letter-spacing: var(--letter-spacing-body);
  color: rgba(26, 26, 26, 0.82);
}

.duration-table {
  margin-top: 34px;
  display: grid;
  grid-template-columns: 88px minmax(0, 1fr);
  column-gap: 32px;
  align-items: start;
}

.duration-table__labels {
  padding-top: 12px;
  display: flex;
  flex-direction: column;
  gap: 36px;
}

.duration-table__labels span {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 19px;
  letter-spacing: var(--letter-spacing-body);
  color: rgba(26, 26, 26, 0.5);
}

.duration-table__columns {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 12px;
}

.duration-card {
  padding: 12px 12px 14px;
  border-radius: 10px;
  background: transparent;
}

.duration-card.is-featured {
  background: rgba(1, 130, 251, 0.18);
}

.duration-card__title {
  margin: 0 0 14px;
  font-weight: var(--font-weight-semibold);
  font-size: 14px;
  line-height: 1;
  letter-spacing: var(--letter-spacing-body);
  color: var(--color-text);
}

.duration-card__copy {
  margin: 0;
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 19px;
  letter-spacing: var(--letter-spacing-body);
  color: var(--color-text);
}

.duration-card__copy + .duration-card__copy {
  margin-top: 18px;
}

.hooks-panel {
  margin-top: 42px;
  display: flex;
  align-items: flex-end;
  gap: 22px;
}

.hooks-table {
  flex: 1 1 auto;
  min-width: 0;
}

.hooks-table__head,
.hooks-row {
  display: grid;
  grid-template-columns: minmax(180px, 1.35fr) repeat(4, minmax(68px, 0.68fr));
  column-gap: 16px;
  align-items: center;
}

.hooks-table__head {
  margin-bottom: 10px;
  padding: 0 12px;
}

.hooks-table__head span {
  font-weight: var(--font-weight-medium);
  font-size: 12px;
  line-height: 1;
  text-align: center;
  color: rgba(26, 26, 26, 0.5);
}

.hooks-table__head span:first-child {
  text-align: left;
}

.hooks-row {
  min-height: 42px;
  padding: 6px 12px;
  border-radius: 8px;
}

.hooks-row + .hooks-row {
  margin-top: 8px;
}

.hooks-row.is-featured {
  background: rgba(1, 130, 251, 0.18);
}

.hooks-row > span {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1;
  text-align: center;
  color: var(--color-text);
}

.hooks-row.is-featured > span {
  font-weight: var(--font-weight-bold);
}

.hooks-row__asset {
  display: flex;
  align-items: center;
  gap: 14px;
}

.hooks-row__asset span {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1;
  color: var(--color-text);
}

.hooks-row__thumb {
  width: 28px;
  height: 28px;
  border-radius: 4px;
  object-fit: cover;
  object-position: center;
  display: block;
}

.hooks-note {
  flex: 0 0 auto;
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 6px;
}

.hooks-note__image {
  width: 46px;
  height: auto;
  display: block;
}

.hooks-note span {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1;
  color: #000000;
}

.faq-visual {
  display: block;
  height: auto;
}

.faq-visual--editing {
  width: 528px;
  margin-top: 42px;
}

.faq-visual--photos {
  width: 574px;
  margin-top: 22px;
}

.faq-process-tag {
  margin-bottom: 26px;
  font-weight: var(--font-weight-semibold);
  font-size: 14px;
  line-height: 1;
  letter-spacing: var(--letter-spacing-body);
  color: var(--color-text);
}

.faq-process-list {
  display: flex;
  flex-direction: column;
  gap: 26px;
}

.faq-process-item__title {
  margin: 0 0 10px;
  font-weight: var(--font-weight-semibold);
  font-size: 14px;
  line-height: 1;
  letter-spacing: var(--letter-spacing-body);
  color: var(--color-text);
}

.faq-process-item__copy {
  margin: 0;
  max-width: 873px;
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.2;
  color: var(--color-text);
}

@media (max-width: 900px) {
  .faq-article {
    padding-top: 48px;
  }

  .faq-grid {
    grid-template-columns: 1fr;
    row-gap: 28px;
  }

  .faq-nav {
    position: sticky;
    top: 0;
    z-index: 2;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 14px 18px;
    padding: 12px 0 16px;
    background: linear-gradient(180deg, #ffffff 0%, rgba(255, 255, 255, 0.94) 100%);
  }

  .faq-nav-link {
    font-size: 16px;
  }

  .faq-title {
    margin-bottom: 72px;
    font-size: 28px;
  }

  .faq-section {
    margin-bottom: 88px;
  }

  .faq-section-heading {
    font-size: 18px;
    line-height: 1.32;
  }

  .duration-table {
    grid-template-columns: 1fr;
    row-gap: 18px;
  }

  .duration-table__labels {
    display: none;
  }

  .duration-table__columns {
    grid-template-columns: 1fr;
  }

  .hooks-panel {
    flex-direction: column;
    align-items: stretch;
  }

  .hooks-table__head {
    display: none;
  }

  .hooks-row {
    grid-template-columns: 1fr 1fr;
    row-gap: 12px;
  }

  .hooks-row__asset {
    grid-column: 1 / -1;
  }

  .hooks-note {
    margin-bottom: 0;
  }

  .faq-visual--editing,
  .faq-visual--photos {
    width: 100%;
    max-width: 100%;
  }
}
</style>
