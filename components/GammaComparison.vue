<script setup>
import { computed, onBeforeUnmount, ref, watch } from 'vue'
import { useSlideContext } from '@slidev/client'

const { $clicks, $renderContext } = useSlideContext()

const scenarios = [
  {
    title: 'Gamma heute',
    investment: 'Keine Zusatzinvestition',
    profit: 18,
    value: 150,
    profitDelta: 'Ausgangswert',
    valueDelta: 'Ausgangswert',
    formula: '18 ÷ 0,12',
    valuation: '150',
    returnFormula: '12 %',
    returnLabel: 'Eigenkapitalkosten im Modell',
    explanation: 'Die jährlichen Cashflows werden als ewige Rente mit 12 % abgezinst.',
    takeaway: 'Der Ausgangspunkt: 150 Mio. $ Wert',
    detail: 'Im Gamma-Modell entsprechen 18 Mio. $ Gewinn dem jährlich ausschüttbaren Cashflow.'
  },
  {
    title: 'Szenario A · Expansion',
    investment: '15 Mio. $ Zusatzinvestition',
    profit: 19.8,
    value: 150,
    profitDelta: '+10 % zum Status quo',
    valueDelta: 'Unverändert',
    formula: '19,8 ÷ 0,12 − 15',
    valuation: '165 − 15 = 150',
    returnFormula: '1,8 ÷ 15 = 12 %',
    returnLabel: 'Rendite = Kapitalkosten',
    explanation: 'Der zusätzliche Cashflow ist genau so viel wert wie die Investition.',
    takeaway: 'Mehr Gewinn. Kein zusätzlicher Wert.',
    detail: 'Die Zusatzinvestition verdient genau die geforderten 12 % Kapitalkosten.'
  },
  {
    title: 'Szenario B · Größere Expansion',
    investment: '30 Mio. $ Zusatzinvestition',
    profit: 20.4,
    value: 140,
    profitDelta: '+13,3 % zum Status quo',
    valueDelta: '−10 Mio. $ zum Status quo',
    formula: '20,4 ÷ 0,12 − 30',
    valuation: '170 − 30 = 140',
    returnFormula: '2,4 ÷ 30 = 8 %',
    returnLabel: 'Rendite < Kapitalkosten (12 %)',
    explanation: 'Der zusätzliche Cashflow ist weniger wert als die Investition.',
    takeaway: 'Höchster Gewinn. Niedrigster Wert.',
    detail: 'Gewinnziel: B wählen. Shareholder-Value-Ziel: Status quo oder A wählen.'
  }
]

const step = computed(() => Math.min(2, Math.max(0, $clicks.value - 1)))
const scenario = computed(() => scenarios[step.value])
const displayedProfit = ref(scenario.value.profit)
const displayedValue = ref(scenario.value.value)
const isInteractive = computed(() => ['slide', 'presenter'].includes($renderContext.value))
const profitText = computed(() => format(displayedProfit.value, step.value === 0 ? 0 : 1))
const valueText = computed(() => format(displayedValue.value, 0))
let frame

function format(value, decimals) {
  return value.toLocaleString('de-DE', {
    minimumFractionDigits: decimals,
    maximumFractionDigits: decimals
  })
}

watch(scenario, next => {
  window.cancelAnimationFrame(frame)
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches || !isInteractive.value) {
    displayedProfit.value = next.profit
    displayedValue.value = next.value
    return
  }

  const fromProfit = displayedProfit.value
  const fromValue = displayedValue.value
  let start
  function animate(time) {
    start ??= time
    const progress = Math.min((time - start) / 650, 1)
    const eased = 1 - (1 - progress) ** 3
    displayedProfit.value = fromProfit + (next.profit - fromProfit) * eased
    displayedValue.value = fromValue + (next.value - fromValue) * eased
    if (progress < 1) frame = window.requestAnimationFrame(animate)
  }
  frame = window.requestAnimationFrame(animate)
})

onBeforeUnmount(() => window.cancelAnimationFrame(frame))
</script>

<template>
  <section
    class="gamma-comparison"
    :class="{ 'is-loss': step === 2 }"
    aria-label="Gamma Inc. im Vergleich"
  >
    <div class="gamma-body">
      <div class="gamma-overview">
        <div :key="step" class="scenario-heading gamma-reveal">
          <h2>{{ scenario.title }}</h2>
          <p>{{ scenario.investment }}</p>
        </div>

        <div class="gamma-metrics" aria-live="polite" aria-atomic="true">
          <div class="metric metric-profit">
            <span class="metric-label">Jährlicher Gewinn</span>
            <div class="metric-value">{{ profitText }} <span>Mio. $</span></div>
            <span class="metric-change" :class="{ 'is-positive': step > 0 }">
              {{ scenario.profitDelta }}
            </span>
          </div>
          <div class="metric metric-value-total">
            <span class="metric-label">Shareholder Value</span>
            <div class="metric-value">{{ valueText }} <span>Mio. $</span></div>
            <span class="metric-change" :class="{ 'is-negative': step === 2 }">
              {{ scenario.valueDelta }}
            </span>
          </div>
        </div>

        <div class="gamma-bars" aria-label="Veränderung gegenüber dem Status quo">
          <div class="bar-label"><span>Gewinn</span><span>0–22 Mio. $</span></div>
          <div class="bar-track profit-track">
            <div
              class="bar-fill profit-fill"
              :style="{ width: `${(scenario.profit / 22) * 100}%` }"
            />
            <span class="baseline" :style="{ left: `${(18 / 22) * 100}%` }" />
          </div>
          <div class="bar-label"><span>Shareholder Value</span><span>0–170 Mio. $</span></div>
          <div class="bar-track value-track">
            <div
              class="bar-fill value-fill"
              :style="{ width: `${(scenario.value / 170) * 100}%` }"
            />
            <span class="baseline" :style="{ left: `${(150 / 170) * 100}%` }" />
          </div>
          <div class="bar-legend"><span />Status quo · unterschiedliche Skalen</div>
        </div>
      </div>

      <aside class="gamma-calculation" aria-live="polite">
        <div :key="step" class="gamma-reveal">
          <p class="calculation-label">So entsteht der Wert</p>
          <p class="calculation-formula">{{ scenario.formula }}</p>
          <p class="calculation-result">{{ scenario.valuation }} <span>Mio. $</span></p>
          <div class="return-comparison">
            <p class="calculation-label">
              {{ step === 0 ? 'Bewertungsmaßstab' : 'Rendite der Zusatzinvestition' }}
            </p>
            <p class="return-formula">{{ scenario.returnFormula }}</p>
            <p class="return-label">{{ scenario.returnLabel }}</p>
          </div>
          <p class="calculation-explanation">{{ scenario.explanation }}</p>
        </div>
      </aside>
    </div>

    <div class="gamma-takeaway" aria-live="polite">
      <div :key="step" class="gamma-reveal">
        <h3>{{ scenario.takeaway }}</h3>
        <p>
          {{ scenario.detail
          }}<Footnote
            text="Rappaport (1999), S. 21–23. Modell: kein Fremdkapital, 40 % Steuern, Vollausschüttung, konstante Cashflows, 12 % Eigenkapitalkosten. Wert nach Abzug der Zusatzinvestition."
          />
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.gamma-comparison {
  --profit-color: #0066b3;
  --value-color: #257b6d;
  display: flex;
  flex: 1;
  min-height: 0;
  flex-direction: column;
  margin-block: -18px 18px;
  color: #253b50;
  line-height: 1.4;
}

.gamma-comparison.is-loss {
  --value-color: #b84b42;
}

:global(.slidev-page:has(.gamma-comparison.slidev-vclick-hidden) .footnote-list) {
  visibility: hidden;
}

.gamma-body {
  display: grid;
  flex: 1;
  grid-template-columns: 1.35fr 1fr;
  gap: 30px;
  align-items: center;
  padding: 7px 0;
}

.scenario-heading h2 {
  margin: 0;
  color: #003978;
  font-size: 21px;
  font-weight: 700;
  line-height: 1.25;
}

.scenario-heading p {
  margin: 3px 0 0;
  color: #73808c;
  font-size: 12px;
  line-height: 1.4;
}

.gamma-metrics {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
  margin: 12px 0;
  font-variant-numeric: tabular-nums;
}

.metric-label {
  display: block;
  color: #536575;
  font-size: 12px;
}

.metric-value {
  margin: 4px 0;
  font-size: 34px;
  font-weight: 700;
  letter-spacing: -1.1px;
  line-height: 1.1;
}

.metric-value span {
  font-size: 15px;
  font-weight: 500;
  letter-spacing: 0;
}

.metric-profit .metric-value {
  color: var(--profit-color);
}

.metric-value-total .metric-value {
  color: var(--value-color);
  transition: color 650ms;
}

.metric-change {
  display: block;
  color: #73808c;
  font-size: 10px;
}

.metric-change.is-positive {
  color: #0066b3;
}

.metric-change.is-negative {
  color: #b84b42;
}

.bar-label {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
  color: #536575;
  font-size: 10px;
}

.bar-label span:last-child {
  color: #7c8995;
  font-size: 9px;
}

.bar-track {
  position: relative;
  height: 11px;
  border-radius: 3px;
  background: #edf1f4;
}

.profit-track {
  margin-bottom: 10px;
}

.bar-fill {
  height: 100%;
  border-radius: inherit;
  transition:
    width 650ms cubic-bezier(0.22, 1, 0.36, 1),
    background-color 650ms;
}

.profit-fill {
  background: var(--profit-color);
}

.value-fill {
  background: var(--value-color);
}

.baseline {
  position: absolute;
  top: -3px;
  bottom: -3px;
  width: 0;
  border-left: 1px dashed #1d354a;
}

.bar-legend {
  display: flex;
  align-items: center;
  gap: 5px;
  margin-top: 7px;
  color: #73808c;
  font-size: 8px;
}

.bar-legend span {
  height: 9px;
  border-left: 1px dashed #1d354a;
}

.gamma-calculation {
  border-left: 1px solid #e0e7ed;
  padding: 0 0 0 27px;
}

.gamma-comparison .calculation-label {
  margin: 0 0 6px;
  color: #73808c;
  font-size: 10px;
  line-height: 1.4;
}

.gamma-comparison .calculation-formula {
  margin: 0 0 5px;
  color: #536575;
  font-size: 17px;
  font-variant-numeric: tabular-nums;
}

.gamma-comparison .calculation-result {
  margin: 0;
  color: #003978;
  font-size: 24px;
  font-weight: 700;
  line-height: 1.3;
}

.calculation-result span {
  font-size: 12px;
  font-weight: 500;
}

.return-comparison {
  margin-top: 16px;
}

.gamma-comparison .return-formula {
  margin: 0 0 3px;
  color: #003978;
  font-size: 21px;
  font-weight: 700;
  line-height: 1.3;
}

.gamma-comparison .return-label {
  margin: 0;
  color: var(--value-color);
  font-size: 11px;
  font-weight: 700;
}

.gamma-comparison .calculation-explanation {
  max-width: 29ch;
  margin: 10px 0 0;
  color: #647584;
  font-size: 12px;
  line-height: 1.5;
}

.gamma-takeaway {
  border-left: 3px solid #0066b3;
  padding: 8px 13px;
  background: #f0f6fb;
  transition:
    background-color 400ms,
    border-color 400ms;
}

.is-loss .gamma-takeaway {
  border-color: #b84b42;
  background: #fcf3f1;
}

.gamma-takeaway h3 {
  margin: 0 0 3px;
  color: #003978;
  font-size: 17px;
  font-weight: 700;
  line-height: 1.25;
}

.gamma-takeaway p {
  margin: 0;
  color: #536575;
  font-size: 12px;
  line-height: 1.4;
}

.gamma-reveal {
  animation: gamma-reveal 300ms ease-out both;
}

@keyframes gamma-reveal {
  from {
    opacity: 0;
    transform: translateY(5px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (prefers-reduced-motion: reduce) {
  .gamma-comparison *,
  .gamma-comparison *::before,
  .gamma-comparison *::after {
    animation: none !important;
    transition: none !important;
  }
}
</style>
