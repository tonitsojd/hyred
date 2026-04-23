<template>
  <div class="nv-header">
    <div class="nv-copy">
      <h1 class="nv-title">New Video</h1>
      <p class="nv-subtitle body-copy">Post a new video assignment for creators.</p>
    </div>

    <div ref="langDropdown" class="nv-lang-dropdown">
      <button
        type="button"
        class="nv-lang-pill interactive-hover"
        :aria-expanded="String(isMenuOpen)"
        aria-haspopup="listbox"
        @click="toggleMenu"
      >
        <span class="nv-lang-label">Language</span>

        <img
          class="nv-flag nv-flag--image"
          :src="selectedCountry.flag"
          :alt="`${selectedCountry.name} flag`"
        >

        <span class="nv-lang-value">{{ selectedCountry.name }}</span>

        <svg
          class="nv-chevron"
          :class="{ 'nv-chevron--open': isMenuOpen }"
          width="16"
          height="16"
          viewBox="0 0 24 24"
          fill="none"
          aria-hidden="true"
        >
          <path
            d="M6 9l6 6 6-6"
            stroke="currentColor"
            stroke-width="2.25"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>

      <div
        v-if="isMenuOpen"
        class="nv-lang-menu"
        role="listbox"
        :aria-activedescendant="`country-${selectedCountry.code}`"
      >
        <button
          v-for="country in countries"
          :id="`country-${country.code}`"
          :key="country.code"
          type="button"
          class="nv-lang-option interactive-hover"
          :class="{ 'nv-lang-option--selected': country.code === selectedCountry.code }"
          role="option"
          :aria-selected="String(country.code === selectedCountry.code)"
          @click="selectCountry(country)"
        >
          <img
            class="nv-flag nv-flag--image"
            :src="country.flag"
            :alt="`${country.name} flag`"
          >
          <span class="nv-lang-option-text">{{ country.name }}</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import flagAustria from '../assets/icons/flags/at 2.svg'
import flagAustralia from '../assets/icons/flags/au 5.svg'
import flagBelgium from '../assets/icons/flags/be 2.svg'
import flagSwitzerland from '../assets/icons/flags/ch 2.svg'
import flagCzech from '../assets/icons/flags/cz 2.svg'
import flagGermany from '../assets/icons/flags/de 2.svg'
import flagDenmark from '../assets/icons/flags/dk 2.svg'
import flagSpain from '../assets/icons/flags/es 2.svg'
import flagFinland from '../assets/icons/flags/fi 2.svg'
import flagFrance from '../assets/icons/flags/fr 2.svg'
import flagUnitedKingdom from '../assets/icons/flags/gb 2.svg'
import flagIreland from '../assets/icons/flags/ie 2.svg'
import flagItaly from '../assets/icons/flags/it 2.svg'
import flagNetherlands from '../assets/icons/flags/nl (1) 2.svg'
import flagNorway from '../assets/icons/flags/no 2.svg'
import flagPortugal from '../assets/icons/flags/pt 2.svg'
import flagSweden from '../assets/icons/flags/se 2.svg'
import flagUnitedStates from '../assets/icons/flags/us 1.svg'

export default {
  name: 'NewVideoHeader',
  data() {
    return {
      isMenuOpen: false,
      selectedCountryCode: 'it',
      countries: [
        { code: 'cz', name: 'Czech', flag: flagCzech },
        { code: 'dk', name: 'Danish', flag: flagDenmark },
        { code: 'be', name: 'Dutch (Belgium)', flag: flagBelgium },
        { code: 'nl', name: 'Dutch', flag: flagNetherlands },
        { code: 'au', name: 'English (Australia)', flag: flagAustralia },
        { code: 'ie', name: 'English (Ireland)', flag: flagIreland },
        { code: 'gb', name: 'English (UK)', flag: flagUnitedKingdom },
        { code: 'us', name: 'English (US)', flag: flagUnitedStates },
        { code: 'fi', name: 'Finnish', flag: flagFinland },
        { code: 'fr', name: 'French', flag: flagFrance },
        { code: 'at', name: 'German (Austria)', flag: flagAustria },
        { code: 'de', name: 'German', flag: flagGermany },
        { code: 'ch', name: 'German (Switzerland)', flag: flagSwitzerland },
        { code: 'it', name: 'Italian', flag: flagItaly },
        { code: 'no', name: 'Norwegian', flag: flagNorway },
        { code: 'pt', name: 'Portuguese', flag: flagPortugal },
        { code: 'es', name: 'Spanish', flag: flagSpain },
        { code: 'se', name: 'Swedish', flag: flagSweden },
      ],
    }
  },
  computed: {
    selectedCountry() {
      return this.countries.find(country => country.code === this.selectedCountryCode) || this.countries[0]
    },
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    selectCountry(country) {
      this.selectedCountryCode = country.code
      this.isMenuOpen = false
    },
    handleDocumentClick(event) {
      const dropdown = this.$refs.langDropdown

      if (dropdown && !dropdown.contains(event.target)) {
        this.isMenuOpen = false
      }
    },
    handleEscape(event) {
      if (event.key === 'Escape') {
        this.isMenuOpen = false
      }
    },
  },
  mounted() {
    document.addEventListener('click', this.handleDocumentClick)
    document.addEventListener('keydown', this.handleEscape)
  },
  beforeDestroy() {
    document.removeEventListener('click', this.handleDocumentClick)
    document.removeEventListener('keydown', this.handleEscape)
  },
}
</script>

<style scoped>
.nv-header {
  width: 100%;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 32px;
}

.nv-copy {
  flex: 1 1 auto;
  min-width: 0;
  padding-top: 2px;
}

.nv-title {
  margin: 0;
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-display);
  line-height: var(--line-height-display);
  letter-spacing: var(--letter-spacing-display);
  color: #16161a;
}

.nv-subtitle {
  margin: 12px 0 0;
  max-width: 320px;
  line-height: var(--line-height-body);
}

.nv-lang-dropdown {
  position: relative;
  flex: 0 0 auto;
}

.nv-lang-pill {
  height: 62px;
  padding: 0 20px;
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-control);
  background: var(--color-surface);
  display: inline-flex;
  align-items: center;
  gap: 10px;
  white-space: nowrap;
  cursor: pointer;
  appearance: none;
  box-shadow: none;
}

.nv-lang-pill::before {
  inset: 0;
  border-radius: inherit;
}

.nv-lang-pill:hover::before,
.nv-lang-pill:focus-visible::before {
  background: rgba(23, 61, 16, 0.08);
}

.nv-lang-label,
.nv-lang-value {
  line-height: 1;
  letter-spacing: var(--letter-spacing-tight);
}

.nv-lang-label {
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-label);
  color: var(--color-text-muted);
}

.nv-lang-value {
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-label);
  color: var(--color-text);
}

.nv-chevron {
  flex: 0 0 auto;
  color: var(--color-text);
  transition: transform 160ms ease;
}

.nv-chevron--open {
  transform: rotate(180deg);
}

.nv-flag {
  flex: 0 0 auto;
}

.nv-flag--image {
  width: 18px;
  height: 18px;
  object-fit: cover;
  display: block;
}

.nv-lang-menu {
  position: absolute;
  top: calc(100% + 10px);
  right: 0;
  z-index: 12;
  width: 290px;
  max-height: 380px;
  padding: 10px;
  border: 1px solid var(--color-border);
  border-radius: 22px;
  background: rgba(255, 255, 255, 0.98);
  box-shadow: 0 20px 54px rgba(17, 20, 28, 0.16);
  overflow-y: auto;
  overscroll-behavior: contain;
}

.nv-lang-menu::-webkit-scrollbar {
  width: 8px;
}

.nv-lang-menu::-webkit-scrollbar-thumb {
  background: rgba(17, 20, 28, 0.18);
  border-radius: 999px;
}

.nv-lang-option {
  width: 100%;
  border: 0;
  background: transparent;
  padding: 12px 14px;
  border-radius: 16px;
  display: flex;
  align-items: center;
  gap: 12px;
  text-align: left;
  cursor: pointer;
}

.nv-lang-option:hover::before,
.nv-lang-option:focus-visible::before {
  background: rgba(23, 61, 16, 0.08);
}

.nv-lang-option--selected {
  background: var(--color-surface-muted);
}

.nv-lang-option--selected:hover::before,
.nv-lang-option--selected:focus-visible::before {
  background: transparent;
}

.nv-lang-option-text {
  font-weight: var(--font-weight-medium);
  font-size: 18px;
  line-height: 1.25;
  letter-spacing: var(--letter-spacing-body);
  color: var(--color-text);
}

@media (max-width: 700px) {
  .nv-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 14px;
  }

  .nv-title {
    font-size: 31px;
    line-height: 1.06;
    letter-spacing: -0.03em;
  }

  .nv-subtitle {
    max-width: none;
    margin-top: 8px;
    font-size: 14px;
    line-height: 1.3;
  }

  .nv-lang-pill {
    height: 48px;
    padding: 0 16px;
    gap: 8px;
    border-radius: 14px;
  }

  .nv-lang-label,
  .nv-lang-value {
    font-size: 14px;
  }

  .nv-lang-menu {
    left: 0;
    right: auto;
    width: min(320px, calc(100vw - 48px));
  }
}
</style>
