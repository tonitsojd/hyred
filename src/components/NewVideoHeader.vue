<template>
  <div class="nv-header">
    <div class="nv-copy">
      <h1 class="nv-title">New Video</h1>
      <p class="nv-subtitle body-copy">Post a new video assignment for creators.</p>
    </div>

    <button type="button" class="nv-lang-pill interactive-hover">
      <span class="nv-lang-label">Language</span>

      <span class="nv-flag" aria-hidden="true">
        <span class="nv-flag-r"></span>
        <span class="nv-flag-w"></span>
        <span class="nv-flag-b"></span>
      </span>

      <span class="nv-lang-value">Dutch</span>

      <svg
        class="nv-chevron"
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
  </div>
</template>

<script>
export default {
  name: 'NewVideoHeader',
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

.nv-lang-pill {
  flex: 0 0 auto;
  height: 62px;
  padding: 0 20px;
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-control);
  background: var(--color-surface);
  display: inline-flex;
  align-items: center;
  gap: 10px;
  white-space: nowrap;
  cursor: default;
  appearance: none;
  box-shadow: none;
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
}

.nv-flag {
  display: inline-flex;
  flex-direction: column;
  width: 18px;
  height: 18px;
  border-radius: 999px;
  overflow: hidden;
  flex: 0 0 auto;
  box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.04);
}

.nv-flag-r,
.nv-flag-w,
.nv-flag-b {
  flex: 1 1 0;
}

.nv-flag-r {
  background: #d44734;
}

.nv-flag-w {
  background: #ffffff;
}

.nv-flag-b {
  background: #29479a;
}

@media (max-width: 700px) {
  .nv-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .nv-subtitle {
    max-width: none;
  }
}
</style>
