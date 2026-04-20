<template>
  <section class="cr-card surface-card">
    <div class="cr-header">
      <div class="cr-copy">
        <div class="cr-heading-row">
          <h2 class="cr-title section-title">Creators</h2>

          <button type="button" class="cr-link inline-action interactive-hover" @click="$emit('open-info', 'creators')">
            <svg class="cr-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true">
              <circle cx="12" cy="12" r="9" stroke="currentColor" stroke-width="1.75" />
              <path d="M12 10.25V16" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" />
              <circle cx="12" cy="7.5" r="1" fill="currentColor" />
            </svg>
            <span class="cr-link-text">Learn More</span>
          </button>
        </div>

        <p class="cr-subtitle body-copy">How many faces you want to run the campaign with?</p>
      </div>

      <div class="cr-counter" aria-label="Creators count">
        <button
          type="button"
          class="cr-counter-btn icon-button-reset interactive-hover"
          aria-label="Decrease creators"
          :disabled="creatorsCount <= minCreators"
          @click="decrementCreators"
        >
          <img :src="minusIcon" alt="" class="cr-counter-icon" />
        </button>

        <span class="cr-counter-value">{{ creatorsCount }}</span>

        <button
          type="button"
          class="cr-counter-btn icon-button-reset interactive-hover"
          aria-label="Increase creators"
          :disabled="creatorsCount >= maxCreators"
          @click="incrementCreators"
        >
          <img :src="plusIcon" alt="" class="cr-counter-icon" />
        </button>
      </div>
    </div>

    <div class="cr-options">
      <div class="cr-option">
        <button
          type="button"
          class="cr-toggle interactive-hover"
          :class="{ 'is-on': hasPerformanceGuarantee }"
          :aria-pressed="String(hasPerformanceGuarantee)"
          :aria-label="hasPerformanceGuarantee ? 'Performance guarantee enabled' : 'Performance guarantee disabled'"
          @click="togglePerformanceGuarantee"
        >
          <span class="cr-toggle-thumb"></span>
        </button>
        <span class="cr-option-text">Get performance guarantee with 3+ creators</span>
      </div>

      <div class="cr-option">
        <button
          type="button"
          class="cr-toggle interactive-hover"
          :class="{ 'is-on': hasFreeCreator }"
          :aria-pressed="String(hasFreeCreator)"
          :aria-label="hasFreeCreator ? 'Free creator enabled' : 'Free creator disabled'"
          @click="toggleFreeCreator"
        >
          <span class="cr-toggle-thumb"></span>
        </button>
        <span class="cr-option-text">Get a free creator with 4+ creators</span>
      </div>
    </div>
  </section>
</template>

<script>
import plusIcon from '@/assets/icons/plus_green.svg'
import minusIcon from '@/assets/icons/minus_green.svg'

export default {
  name: 'CreatorsCard',
  emits: ['open-info'],
  data() {
    return {
      creatorsCount: 5,
      minCreators: 1,
      maxCreators: 10,
      plusIcon,
      minusIcon,
    }
  },
  computed: {
    hasPerformanceGuarantee() {
      return this.creatorsCount >= 3
    },
    hasFreeCreator() {
      return this.creatorsCount >= 4
    },
  },
  methods: {
    decrementCreators() {
      if (this.creatorsCount > this.minCreators) {
        this.creatorsCount -= 1
      }
    },
    incrementCreators() {
      if (this.creatorsCount < this.maxCreators) {
        this.creatorsCount += 1
      }
    },
    togglePerformanceGuarantee() {
      if (this.creatorsCount <= 2) {
        this.creatorsCount = 3
      }
    },
    toggleFreeCreator() {
      if (this.creatorsCount <= 3) {
        this.creatorsCount = 4
      }
    },
  },
}
</script>
<style scoped>
.cr-card {
  position: relative;
}

.cr-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 24px;
}

.cr-copy {
  min-width: 0;
  flex: 1 1 auto;
}

.cr-heading-row {
  display: flex;
  align-items: center;
  gap: 16px;
  flex-wrap: wrap;
}

.cr-icon {
  flex: 0 0 auto;
  color: var(--color-text-soft);
}

.cr-link-text {
  color: var(--color-text-soft);
  font-weight: var(--font-weight-medium);
}

.cr-subtitle {
  margin: 8px 0 0;
}

.cr-counter {
  flex: 0 0 auto;
  width: 110px;
  height: 52px;
  border-radius: var(--radius-sm);
  background: var(--color-accent);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  padding: 0 10px;
}

.cr-counter-btn {
  width: 28px;
  height: 28px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 999px;
}

.cr-counter-btn:disabled {
  opacity: 0.45;
}

.cr-counter-icon {
  display: block;
  width: 16px;
  height: 16px;
}

.cr-counter-value {
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-title-sm);
  line-height: var(--line-height-title-sm);
  letter-spacing: var(--letter-spacing-tight);
  color: #ffffff;
  padding: 0 8px;
}

.cr-counter-btn::before {
  inset: 0;
  border-radius: 999px;
}

.cr-counter-btn:hover::before,
.cr-counter-btn:focus-visible::before {
  background: rgba(255, 255, 255, 0.2);
}

.cr-options {
  margin-top: 24px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.cr-option {
  min-height: 56px;
  border-radius: var(--radius-sm);
  background: var(--color-surface-muted);
  padding: 16px;
  display: flex;
  align-items: center;
  gap: 16px;
}

.cr-toggle {
  flex: 0 0 auto;
  width: 44px;
  height: 24px;
  border: 0;
  border-radius: var(--radius-pill);
  padding: 2px;
  background: rgba(23, 61, 16, 0.22);
  display: flex;
  align-items: center;
  justify-content: flex-start;
  cursor: default;
  transition: background-color 160ms ease, justify-content 160ms ease;
}

.cr-toggle::before {
  inset: 0;
  border-radius: var(--radius-pill);
}

.cr-toggle:hover::before,
.cr-toggle:focus-visible::before {
  background: rgba(255, 255, 255, 0.2);
}

.cr-toggle.is-on {
  background: var(--color-accent);
  justify-content: flex-end;
}

.cr-toggle-thumb {
  display: block;
  width: 20px;
  height: 20px;
  border-radius: var(--radius-pill);
  background: var(--color-surface);
}

.cr-option-text {
  min-width: 0;
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-body);
  line-height: 20px;
  letter-spacing: var(--letter-spacing-body);
  color: var(--color-text);
}

@media (max-width: 700px) {
  .cr-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .cr-counter {
    width: 160px;
    height: 52px;
    padding: 0 20px;
  }

  .cr-option {
    align-items: flex-start;
  }
}
</style>
