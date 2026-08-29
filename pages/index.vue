<script setup>
const features = [
  {
    title: 'Design moderne',
    text: 'Une identité visuelle claire, premium et facile à faire évoluer selon votre marque.'
  },
  {
    title: 'Rapidité',
    text: 'Une expérience fluide et optimisée pour les visiteurs sur mobile et desktop.'
  },
  {
    title: 'Conversion',
    text: 'Des sections orientées action pour guider les utilisateurs vers un objectif précis.'
  }
]

const steps = [
  'Analyse de votre objectif',
  'Mise en place du concept',
  'Design et contenu',
  'Lancement et optimisation'
]

const testimonials = [
  {
    quote: 'Une présence digitale plus claire et beaucoup plus professionnelle.',
    author: 'Sophie M.'
  },
  {
    quote: 'Le site donne immédiatement une image premium à notre activité.',
    author: 'Lucas D.'
  }
]

const metrics = [
  { end: 120, decimals: 0, suffix: '+', label: 'Projets' },
  { end: 4.9, decimals: 1, suffix: '/5', label: 'Clients' },
  { end: 30, decimals: 0, suffix: '%', label: 'Plus de leads' }
]

const metricValues = ref(metrics.map(() => 0))

function formatMetric(index) {
  return metricValues.value[index].toFixed(metrics[index].decimals)
}

onMounted(() => {
  const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches

  if (reduceMotion) {
    metricValues.value = metrics.map((m) => m.end)
  } else {
    const duration = 1200
    const start = performance.now()

    const tick = (now) => {
      const progress = Math.min((now - start) / duration, 1)
      const eased = 1 - Math.pow(1 - progress, 3)
      metricValues.value = metrics.map((m) => m.end * eased)
      if (progress < 1) requestAnimationFrame(tick)
    }

    requestAnimationFrame(tick)
  }

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('in-view')
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.15 }
  )

  document.querySelectorAll('.reveal').forEach((el) => observer.observe(el))
})
</script>

<template>
  <div class="page-shell">
    <header class="topbar">
      <div class="brand">Demo</div>
      <nav class="nav">
        <a href="#services">Services</a>
        <a href="#process">Process</a>
        <a href="#avis">Avis</a>
        <a href="#contact" class="nav-cta">Contact</a>
      </nav>
    </header>

    <main>
      <section class="hero">
        <div class="hero-copy">
          <span class="eyebrow">Agence digitale</span>
          <h1>On donne une présence premium à votre business.</h1>
          <p>
            Nous concevons des sites modernes, lisibles et efficaces pour aider votre marque à gagner
            en visibilité et en confiance.
          </p>
          <div class="hero-actions">
            <a href="#contact" class="btn btn-primary">Démarrer</a>
            <a href="#services" class="btn btn-secondary">Voir les services</a>
          </div>
          <ul class="metrics">
            <li v-for="(metric, index) in metrics" :key="metric.label">
              <strong>{{ formatMetric(index) }}{{ metric.suffix }}</strong>
              <span>{{ metric.label }}</span>
            </li>
          </ul>
        </div>

        <div class="hero-card">
          <div class="mini-panel">
            <span class="mini-label">Performance</span>
            <strong>+82%</strong>
            <small>Engagement utilisateur</small>
          </div>
          <div class="chart-box">
            <span />
            <span />
            <span />
            <span />
            <span />
          </div>
        </div>
      </section>

      <section id="services" class="section">
        <div class="section-heading reveal">
          <span class="eyebrow">Nos services</span>
          <h2>Ce qu’on peut construire ensemble</h2>
        </div>

        <div class="feature-grid reveal">
          <article v-for="(feature, index) in features" :key="feature.title" class="feature-card">
            <div class="icon">{{ String(index + 1).padStart(2, '0') }}</div>
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.text }}</p>
          </article>
        </div>
      </section>

      <section id="process" class="section alt">
        <div class="section-heading reveal">
          <span class="eyebrow">Processus</span>
          <h2>Une méthode simple et efficace</h2>
        </div>

        <div class="steps reveal">
          <div v-for="(step, index) in steps" :key="step" class="step-item">
            <span>{{ index + 1 }}</span>
            <p>{{ step }}</p>
          </div>
        </div>
      </section>

      <section id="avis" class="section">
        <div class="section-heading reveal">
          <span class="eyebrow">Témoignages</span>
          <h2>Ce que nos clients disent</h2>
        </div>

        <div class="testimonial-grid reveal">
          <article v-for="item in testimonials" :key="item.author" class="quote-card">
            <p>“{{ item.quote }}”</p>
            <strong>{{ item.author }}</strong>
          </article>
        </div>
      </section>

      <section id="contact" class="section">
        <div class="cta-box reveal">
          <div>
            <h2>Prêt à lancer votre prochain projet ?</h2>
            <p>Parlons de votre idée et créons un site qui vous ressemble.</p>
          </div>
          <a href="mailto:hello@demo.wg" class="btn btn-primary">hello@demo.wg</a>
        </div>
      </section>
    </main>

    <footer class="footer">
      <div class="footer-main">
        <div class="footer-brand">
          <span class="brand">Demo</span>
          <p>Agence digitale : des sites modernes, lisibles et efficaces pour votre marque.</p>
        </div>
        <div class="footer-col">
          <h4>Navigation</h4>
          <ul>
            <li><a href="#services">Services</a></li>
            <li><a href="#process">Process</a></li>
            <li><a href="#avis">Avis</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h4>Contact</h4>
          <ul>
            <li><a href="mailto:hello@demo.wg">hello@demo.wg</a></li>
            <li>Paris, France</li>
          </ul>
        </div>
      </div>
      <div class="footer-bottom">
        <span>© 2026 Demo. Tous droits réservés.</span>
        <span>Site de démonstration</span>
      </div>
    </footer>
  </div>
</template>
