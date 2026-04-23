<template>
  <section class="customize-popup" role="dialog" aria-modal="true" aria-label="Customise your video">
    <header class="customize-popup__header">
      <h2 class="customize-popup__title">Customise your video</h2>
      <button
        type="button"
        class="customize-popup__close icon-button-reset interactive-hover"
        aria-label="Close customise video popup"
        @click="$emit('close')"
      >
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" aria-hidden="true">
          <path d="M4 4L20 20" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
          <path d="M20 4L4 20" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
        </svg>
      </button>
    </header>

    <div class="customize-popup__body">
      <div class="customize-row">
        <div class="customize-row__copy">
          <h3 class="customize-row__title">Duration = {{ selectedDuration.label }}</h3>
          <p class="customize-row__subtitle">{{ selectedDuration.description }}</p>
        </div>

        <div class="customize-row__control customize-row__control--split">
          <div class="stepper stepper--duration">
            <button type="button" class="stepper__button icon-button-reset interactive-hover" aria-label="Decrease duration" @click="decrementDuration">
              <img src="../assets/icons/minus.svg" alt="" class="stepper__icon" aria-hidden="true">
            </button>
            <span class="stepper__value">{{ selectedDuration.value }}</span>
            <button type="button" class="stepper__button icon-button-reset interactive-hover" aria-label="Increase duration" @click="incrementDuration">
              <img src="../assets/icons/plus.svg" alt="" class="stepper__icon" aria-hidden="true">
            </button>
          </div>
          <span class="customize-row__price">€99</span>
        </div>
      </div>

      <div class="customize-row">
        <div class="customize-row__copy">
          <h3 class="customize-row__title">Hooks</h3>
          <p class="customize-row__subtitle">One video + multiple intros = best ROI</p>
        </div>

        <div class="customize-row__control customize-row__control--split">
          <div class="stepper">
            <button type="button" class="stepper__button icon-button-reset interactive-hover" aria-label="Decrease hooks" @click="decrementHooks">
              <img src="../assets/icons/minus.svg" alt="" class="stepper__icon" aria-hidden="true">
            </button>
            <span class="stepper__value">{{ hooksCount }}</span>
            <button type="button" class="stepper__button icon-button-reset interactive-hover" aria-label="Increase hooks" @click="incrementHooks">
              <img src="../assets/icons/plus.svg" alt="" class="stepper__icon" aria-hidden="true">
            </button>
          </div>
          <span class="customize-row__price">€48</span>
        </div>
      </div>

      <div class="customize-row">
        <div class="customize-row__copy">
          <h3 class="customize-row__title">Editing</h3>
          <p class="customize-row__subtitle">Our team turns video files into the final product</p>
        </div>

        <div class="customize-row__control customize-row__control--split">
          <button
            type="button"
            class="customize-toggle icon-button-reset interactive-hover"
            :class="{ 'is-on': editingEnabled }"
            :aria-pressed="String(editingEnabled)"
            aria-label="Toggle editing"
            @click="editingEnabled = !editingEnabled"
          >
            <span class="customize-toggle__thumb"></span>
          </button>
          <span class="customize-row__price">€79</span>
        </div>
      </div>

      <div class="customize-row">
        <div class="customize-row__copy">
          <h3 class="customize-row__title">Photos</h3>
          <p class="customize-row__subtitle">For all the other pieces of your campaign</p>
        </div>

        <div class="customize-row__control customize-row__control--split">
          <div class="stepper">
            <button type="button" class="stepper__button icon-button-reset interactive-hover" aria-label="Decrease photos" @click="decrementPhotos">
              <img src="../assets/icons/minus.svg" alt="" class="stepper__icon" aria-hidden="true">
            </button>
            <span class="stepper__value">{{ photosCount }}</span>
            <button type="button" class="stepper__button icon-button-reset interactive-hover" aria-label="Increase photos" @click="incrementPhotos">
              <img src="../assets/icons/plus.svg" alt="" class="stepper__icon" aria-hidden="true">
            </button>
          </div>
          <span class="customize-row__price">€79</span>
        </div>
      </div>

      <div class="customize-popup__actions">
        <button type="button" class="customize-popup__reset icon-button-reset interactive-hover" @click="resetToDefault">Back to Default</button>
      </div>
    </div>

    <footer class="customize-popup__footer">
      <span class="customize-popup__footer-label">Price per video</span>
      <span class="customize-popup__footer-value">€226</span>
    </footer>
  </section>
</template>

<script>
import plusIcon from '@/assets/icons/plus.svg'
import minusIcon from '@/assets/icons/minus.svg'

const DEFAULT_DURATION_INDEX = 1
const DEFAULT_HOOKS = 2
const DEFAULT_PHOTOS = 2
const DEFAULT_EDITING = true

export default {
  name: 'CustomizeVideoPopup',
  emits: ['close'],
  data() {
    return {
      durationIndex: DEFAULT_DURATION_INDEX,
      hooksCount: DEFAULT_HOOKS,
      photosCount: DEFAULT_PHOTOS,
      editingEnabled: DEFAULT_EDITING,
      plusIcon,
      minusIcon,
      durationOptions: [
        { value: '15s', label: '15 seconds', description: 'Short intro - problem, product, and CTA' },
        { value: '30s', label: '30 seconds', description: 'Full length - intro, story, and CTA' },
        { value: '60s', label: '60 seconds', description: 'Extended format - tutorial, context, and CTA' },
      ],
    }
  },
  computed: {
    selectedDuration() {
      return this.durationOptions[this.durationIndex]
    },
  },
  methods: {
    decrementDuration() {
      if (this.durationIndex > 0) {
        this.durationIndex -= 1
      }
    },
    incrementDuration() {
      if (this.durationIndex < this.durationOptions.length - 1) {
        this.durationIndex += 1
      }
    },
    decrementHooks() {
      if (this.hooksCount > 1) {
        this.hooksCount -= 1
      }
    },
    incrementHooks() {
      if (this.hooksCount < 9) {
        this.hooksCount += 1
      }
    },
    decrementPhotos() {
      if (this.photosCount > 1) {
        this.photosCount -= 1
      }
    },
    incrementPhotos() {
      if (this.photosCount < 9) {
        this.photosCount += 1
      }
    },
    resetToDefault() {
      this.durationIndex = DEFAULT_DURATION_INDEX
      this.hooksCount = DEFAULT_HOOKS
      this.photosCount = DEFAULT_PHOTOS
      this.editingEnabled = DEFAULT_EDITING
    },
  },
}
</script>

<style scoped>
.customize-popup {
  width: 556px;
  max-width: 100%;
  border: 1px solid rgba(51, 51, 51, 0.25);
  border-radius: 12px;
  background: var(--color-surface);
  overflow: hidden;
  box-shadow: 0 26px 80px rgba(15, 23, 42, 0.16);
}

.customize-popup__header,
.customize-row,
.customize-popup__footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  padding: 20px;
  border-bottom: 1px solid rgba(51, 51, 51, 0.25);
}

.customize-popup__title {
  margin: 0;
  font-weight: var(--font-weight-medium);
  font-size: 16px;
  line-height: 1.2;
  color: var(--color-text);
}

.customize-popup__close {
  color: var(--color-text);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-left: auto;
}

.customize-row__copy {
  min-width: 0;
}

.customize-row__title {
  margin: 0;
  font-weight: var(--font-weight-medium);
  font-size: 16px;
  line-height: 1.2;
  color: var(--color-text);
}

.customize-row__subtitle {
  margin: 8px 0 0;
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.2;
  color: #929292;
}

.customize-row__control {
  flex: 0 0 auto;
}

.customize-row__control--split {
  display: flex;
  align-items: center;
  gap: 16px;
}

.stepper {
  min-width: 97px;
  height: 41px;
  padding: 0 12px;
  border: 1px solid #dddddd;
  border-radius: 5px;
  background: #f5f5f5;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
}

.stepper__button,
.stepper__value {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1;
  color: var(--color-text);
}

.stepper__button {
  width: 12px;
  text-align: center;
}

.stepper__icon {
  display: block;
  width: 36px;
  height: 36px;
  object-fit: contain;
}

.customize-toggle {
  width: 44px;
  height: 24px;
  padding: 2px;
  border-radius: var(--radius-pill);
  background: rgba(26, 26, 26, 0.18);
  display: inline-flex;
  align-items: center;
  justify-content: flex-start;
  transition: background-color 160ms ease, justify-content 160ms ease;
}

.customize-toggle.is-on {
  background: #1a1a1a;
  justify-content: flex-end;
}

.customize-toggle__thumb {
  width: 20px;
  height: 20px;
  border-radius: var(--radius-pill);
  background: #ffffff;
  display: block;
}

.customize-row__price,
.customize-popup__footer-label,
.customize-popup__footer-value {
  font-weight: var(--font-weight-semibold);
  font-size: 16px;
  line-height: 1.2;
  color: var(--color-text);
}

.customize-popup__actions {
  padding: 20px;
  border-bottom: 1px solid rgba(51, 51, 51, 0.25);
  display: flex;
  justify-content: center;
}

.customize-popup__reset {
  min-height: 52px;
  padding: 16px 24px;
  border-radius: 26px;
  background: var(--color-surface-muted);
  font-weight: var(--font-weight-medium);
  font-size: 16px;
  line-height: 1.2;
  color: var(--color-text);
}

@media (max-width: 640px) {
  .customize-popup {
    width: 100%;
  }

  .customize-row,
  .customize-popup__footer {
    align-items: flex-start;
    flex-direction: column;
  }

  .customize-popup__header {
    align-items: center;
    flex-direction: row;
  }

  .customize-row__control--split {
    width: 100%;
    justify-content: space-between;
  }
}
</style>
