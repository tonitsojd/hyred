<template>
  <section class="co-card surface-card">
    <div class="co-top">
      <div class="co-left">
        <h2 class="co-title section-title">Checkout</h2>
        <p class="co-copy body-copy body-copy--muted">
          Deposit the budget to start
          attracting creators. 100% refund
          if you change your mind.
        </p>
      </div>

      <div class="co-right">
        <div class="co-row">
          <span class="co-label">Videos =</span>
          <span class="co-value">€226 × 5 = €1130</span>
        </div>

        <div class="co-row">
          <span class="co-label">Performance guarantee =</span>
          <span class="co-value">€0</span>
        </div>

        <div class="co-row">
          <span class="co-label">Free Creator =</span>
          <span class="co-value">€226 Off</span>
        </div>

        <div class="co-row co-row-total">
          <span class="co-label">Total =</span>
          <span class="co-mid">1130 − 226 =</span>
          <span class="co-total">€906</span>
        </div>
      </div>
    </div>

    <div class="co-bottom">
      <button type="button" class="co-button interactive-hover">Checkout</button>
      <div class="co-refund">100% Refund if you don’t like the creators</div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'CheckoutCard',
}
</script>

<style scoped>
.co-card {
  position: relative;
}

.co-top {
  display: flex;
  gap: 24px;
}

.co-left,
.co-right {
  width: calc(50% - 12px);
}

.co-copy {
  margin: 8px 0 0;
}

.co-right {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.co-row {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  gap: 16px;
}

.co-label,
.co-value,
.co-mid {
  font-weight: var(--font-weight-medium);
  font-size: var(--font-size-body);
  line-height: var(--line-height-label);
  letter-spacing: var(--letter-spacing-body);
}

.co-label {
  color: var(--color-text-soft);
  white-space: nowrap;
}

.co-value,
.co-mid {
  color: var(--color-text);
  text-align: right;
}

.co-row-total .co-label,
.co-row-total .co-mid {
  color: var(--color-text);
}

.co-total {
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-title-sm);
  line-height: var(--line-height-title-sm);
  letter-spacing: var(--letter-spacing-tight);
  color: var(--color-text);
  white-space: nowrap;
}

.co-bottom {
  margin-top: 24px;
  border-radius: 24px;
  overflow: hidden;
  background: var(--color-surface-muted);
}

.co-button {
  width: 100%;
  height: 82px;
  border: 0;
  border-radius: 24px;
  background: var(--color-accent);
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-heading);
  line-height: var(--line-height-heading);
  letter-spacing: var(--letter-spacing-heading);
  color: var(--color-accent-contrast);
  cursor: default;
}

.co-button::before {
  inset: 0;
  border-radius: 24px;
}

.co-button:hover::before,
.co-button:focus-visible::before {
  background: rgba(255, 255, 255, 0.2);
}

.co-refund {
  min-height: 74px;
  padding: 18px 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-weight: var(--font-weight-semibold);
  font-size: var(--font-size-title-sm);
  line-height: var(--line-height-title-sm);
  letter-spacing: var(--letter-spacing-tight);
  color: rgba(26, 26, 26, 0.62);
}

@media (max-width: 700px) {
  .co-card {
    padding: 14px;
  }

  .co-top {
    flex-direction: column;
    gap: 16px;
  }

  .co-left,
  .co-right {
    width: 100%;
  }

  .co-copy {
    margin-top: 8px;
    max-width: 238px;
    line-height: 1.28;
  }

  .co-right {
    gap: 10px;
  }

  .co-row {
    flex-wrap: nowrap;
    gap: 12px;
  }

  .co-label,
  .co-value,
  .co-mid {
    font-size: 14px;
    line-height: 1.25;
  }

  .co-label {
    white-space: normal;
  }

  .co-value,
  .co-mid {
    margin-left: auto;
    white-space: nowrap;
  }

  .co-row-total {
    align-items: baseline;
  }

  .co-total {
    font-size: 16px;
  }

  .co-button {
    height: 44px;
    border-radius: 14px;
    font-size: 16px;
    line-height: 1;
  }

  .co-bottom {
    margin-top: 18px;
    border-radius: 16px;
  }

  .co-refund {
    min-height: 60px;
    padding: 14px 20px;
    font-size: 12px;
    line-height: 1.3;
  }
}
</style>
