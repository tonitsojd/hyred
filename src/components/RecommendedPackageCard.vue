<template>
  <section class="rp-card surface-card">
    <div class="rp-top">
      <div class="rp-main">
        <h2 class="rp-title section-title">Recommended Package</h2>
        <p class="rp-subtitle body-copy">Optimal price to performance for new users.</p>
      </div>

      <div class="rp-actions">
        <button type="button" class="rp-link inline-action interactive-hover" @click="$emit('open-info', 'duration')">
          <svg class="rp-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true">
            <circle cx="12" cy="12" r="9" stroke="currentColor" stroke-width="1.75" />
            <path d="M12 10.25V16" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" />
            <circle cx="12" cy="7.5" r="1" fill="currentColor" />
          </svg>
          <span class="rp-link-text">What is this?</span>
        </button>

        <button type="button" class="rp-link inline-action interactive-hover" @click="$emit('open-edit')">
          <svg class="rp-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true">
            <path
              d="M4 20h4.25L19 9.25 14.75 5 4 15.75V20Z"
              stroke="currentColor"
              stroke-width="1.75"
              stroke-linejoin="round"
            />
            <path
              d="M12.75 7 17 11.25"
              stroke="currentColor"
              stroke-width="1.75"
              stroke-linecap="round"
            />
          </svg>
          <span class="rp-link-text">Edit</span>
        </button>
      </div>
    </div>

    <div class="rp-breakdown">
      <div class="rp-item">
        <div class="rp-body">3 intros</div>
        <div class="rp-body">€79</div>
      </div>

      <div class="rp-operator">
        <img :src="plusIcon" alt="" class="rp-op-icon" />
      </div>

      <div class="rp-item">
        <div class="rp-body">30 seconds</div>
        <div class="rp-body">€79</div>
      </div>

      <div class="rp-operator">
        <img :src="plusIcon" alt="" class="rp-op-icon" />
      </div>

      <div class="rp-item">
        <div class="rp-body">Editing</div>
        <div class="rp-body">€79</div>
      </div>

      <div class="rp-operator">
        <img :src="equalsIcon" alt="" class="rp-op-icon" />
      </div>

      <div class="rp-total">
        <div class="rp-body">Total</div>
        <div class="rp-total-value">€226</div>
      </div>
    </div>
  </section>
</template>

<script>
import plusIcon from '@/assets/icons/plus.svg'
import equalsIcon from '@/assets/icons/equals.svg'

export default {
  name: 'RecommendedPackageCard',
  emits: ['open-info', 'open-edit'],
  data() {
    return {
      plusIcon,
      equalsIcon,
    }
  },
}
</script>

<style scoped>
.rp-card {
  position: relative;
}

.rp-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 20px;
}

.rp-main {
  min-width: 0;
  flex: 1 1 auto;
}

.rp-subtitle {
  margin: 8px 0 0;
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.005em;
}

.rp-actions {
  flex: 0 0 auto;
  display: inline-flex;
  align-items: center;
  gap: 18px;
  padding-top: 2px;
}

.rp-icon {
  flex: 0 0 auto;
  color: var(--color-text-soft);
}

.rp-link {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.005em;
}

.rp-link-text {
  color: var(--color-text-soft);
}

.rp-breakdown {
  margin-top: 24px;
  padding: 12px 24px;
  min-height: 79px;
  border-radius: var(--radius-sm);
  background: var(--color-surface-muted);
  display: grid;
  grid-template-columns: 1fr auto 1fr auto 1fr auto 1fr;
  align-items: center;
  column-gap: 24px;
}

.rp-item,
.rp-total {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 4px;
  min-width: 0;
}

.rp-total {
  align-items: flex-end;
  text-align: right;
}

.rp-operator {
  display: flex;
  align-items: center;
  justify-content: center;
}

.rp-op-icon {
  width: 16px;
  height: 16px;
  object-fit: contain;
  display: block;
}

.rp-body {
  font-weight: var(--font-weight-medium);
  font-size: 14px;
  line-height: 1.2;
  letter-spacing: -0.005em;
  color: var(--color-text);
  white-space: nowrap;
}

.rp-total-value {
  font-weight: var(--font-weight-semibold);
  font-size: 16px;
  line-height: 1.2;
  letter-spacing: -0.02em;
  color: var(--color-text);
  white-space: nowrap;
}

@media (max-width: 700px) {
  .rp-top {
    flex-direction: column;
    align-items: flex-start;
  }

  .rp-actions {
    padding-top: 0;
  }

  .rp-breakdown {
    grid-template-columns: 1fr;
    row-gap: 16px;
  }

  .rp-operator {
    justify-content: flex-start;
  }

  .rp-total {
    align-items: flex-start;
    text-align: left;
  }
}
</style>
