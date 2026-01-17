# 🌐 Landing Page Specification (Web-Only)

## Overview

**Purpose**: Waitlist signup only (no app preview, no features)  
**Stack**: Next.js (static export) or simple HTML + Vercel  
**Performance**: <3s load, 100 Lighthouse score  
**Mobile**: Fully responsive, landing page FIRST  

---

## Page Structure (Single Page)

```
Homepage (vera.app)
│
├── Hero Section (Hero CTA)
│   ├── H1: "Çocuğun Büyümesini Duygusal Anılarla Sakla"
│   ├── Subheading: "Yıllık fiziksel albüm, dijital hayat arşivi"
│   └── CTA Button: "✨ Beta'ya Katıl (Ücretsiz) ✨"
│
├── Pain Points (3 columns)
│   ├── Fotoğraf dağınıklığı
│   ├── Aile paylaşımı zorluk
│   └── Fiziksel albüm yapamama
│
├── Solution Section
│   ├── Step 1: Upload
│   ├── Step 2: Story
│   ├── Step 3: Albüm
│   └── Step 4: Repeat
│
├── Features (6 items)
│   ├── Milestones
│   ├── Memory Cards
│   ├── Family Sharing
│   ├── Physical Album
│   ├── Long-term Archive
│   └── Surprise Moments
│
├── Pricing (3 tiers)
│   ├── Standart: ₺999
│   ├── Premium: ₺1,999
│   └── VIP: ₺4,999
│
├── Testimonials (2-3 quotes)
│   └── "Ağladım" vibes
│
├── FAQ (5-7 questions)
│   ├── "Verilerim güvenli mi?"
│   ├── "Albüm ne zaman gelir?"
│   ├── "İptal edebilir miyim?"
│   ├── "Aile paylaşımı nasıl?"
│   ├── "Fotoğraf limiti var mı?"
│   ├── "İngilizce desteği?"
│   └── "Kime iletişim kurayım?"
│
├── Final CTA Section
│   └── "100 kişi ücretsiz, sonrası normal fiyat"
│
├── Footer
│   ├── Links: Privacy, Terms, Contact
│   ├── Social: Instagram, TikTok
│   └── Email: support@vera.app
│
└── Email Capture Modal
    └── (Exit intent: "Haberleri kaçırma!")
```

---

## HTML Structure (Minimal Version)

```html
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Vera | Çocuğun Hayatını Albüme Çevirin</title>
  <meta name="description" content="Yıllık fiziksel albüm + dijital hayat arşivi. Doğumdan 18 yaşına kadar hatıralar.">
  <meta property="og:image" content="og-image.jpg">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<!-- HERO -->
<section class="hero">
  <nav class="navbar">
    <div class="logo">Vera</div>
    <div class="nav-links">
      <a href="#features">Özellikler</a>
      <a href="#pricing">Fiyat</a>
      <a href="#faq">SSS</a>
    </div>
  </nav>

  <div class="hero-content">
    <h1>Çocuğun Büyümesini Duygusal Anılarla Sakla</h1>
    <p class="subtitle">Yıllık fiziksel albüm + dijital hayat arşivi. Doğumdan 18 yaşına kadar hatıralar.</p>
    
    <button class="cta-button" onclick="scrollToSignup()">
      ✨ Beta'ya Katıl (Ücretsiz) ✨
    </button>
    
    <p class="hero-subtext">🎁 İlk 100 kullanıcı: Yıl 1'de TAMAMEN ÜCRETSİZ + ₺200 albüm kredisi</p>
  </div>

  <div class="hero-image">
    <img src="hero.png" alt="Family with albums" loading="lazy">
  </div>
</section>

<!-- PAIN POINTS -->
<section class="pain-points">
  <h2>Senin Sorunu</h2>
  
  <div class="grid-3">
    <div class="card">
      <h3>📱 10.000 Fotoğraf, Hiçbir Anlam</h3>
      <p>Hangisi ne zaman? Bağlam kayboldu. Duygular unutuldu.</p>
    </div>
    <div class="card">
      <h3>👪 Aile Paylaşımı Gerçekten Zor</h3>
      <p>WhatsApp'ta kayboluyor. Babanne eksik kalıyor.</p>
    </div>
    <div class="card">
      <h3>🖼️ Fiziksel Albüm Yapamıyorsun</h3>
      <p>"Bir gün yaparım" ama 5 yıl geçti. Hayat çok hızlı.</p>
    </div>
  </div>
</section>

<!-- SOLUTION -->
<section class="solution">
  <h2>Vera'nın Çözümü: 4 Adım</h2>
  
  <div class="steps">
    <div class="step">
      <div class="step-number">1</div>
      <h3>Fotoğraf Yükle</h3>
      <p>5 dakikada toplu upload. Otomatik tarih ve yaş hesaplama.</p>
    </div>
    <div class="step">
      <div class="step-number">2</div>
      <h3>Hikaye Ekle</h3>
      <p>Her fotoğraf bir anı: "İlk adımını attı 🎉"</p>
    </div>
    <div class="step">
      <div class="step-number">3</div>
      <h3>Yıl Sonunda Albüm</h3>
      <p>Kasım'da preview, Aralık'ta kapıda fiziksel albüm.</p>
    </div>
    <div class="step">
      <div class="step-number">4</div>
      <h3>Döngü Yeniden Başla</h3>
      <p>Ocak'ta yeni yıl, yeni albüm. 18 yaşına kadar her yıl.</p>
    </div>
  </div>
</section>

<!-- FEATURES -->
<section class="features" id="features">
  <h2>Vera'nın Güçlü Yanları</h2>
  
  <div class="grid-3">
    <div class="feature">
      <div class="feature-icon">🎉</div>
      <h3>Milestone Celebrations</h3>
      <p>İlk adım, ilk diş, doğum günü otomatik anılar</p>
    </div>
    <div class="feature">
      <div class="feature-icon">💝</div>
      <h3>Memory Cards</h3>
      <p>"2 yıl öncesine bugün" push notifications</p>
    </div>
    <div class="feature">
      <div class="feature-icon">🔐</div>
      <h3>Uzun Vadeli Arşiv</h3>
      <p>Vera kapanmayacak. Verini sonsuza kadar tutacak.</p>
    </div>
    <div class="feature">
      <div class="feature-icon">👪</div>
      <h3>Aile Paylaşımı</h3>
      <p>Babanne, babaanneyi davet et. Her yıl albüm alabilir.</p>
    </div>
    <div class="feature">
      <div class="feature-icon">📖</div>
      <h3>Fiziksel Albüm</h3>
      <p>Elinde tutulacak kadar gerçek, her yıl.</p>
    </div>
    <div class="feature">
      <div class="feature-icon">✨</div>
      <h3>Açılmaz Anılar</h3>
      <p>Random fotoğraf sürprizi her hafta.</p>
    </div>
  </div>
</section>

<!-- PRICING -->
<section class="pricing" id="pricing">
  <h2>Fiyatlandırma (Beta Sonrası)</h2>
  
  <div class="pricing-grid">
    <div class="price-card">
      <h3>Standart</h3>
      <div class="price">₺999/yıl</div>
      <ul>
        <li>✅ Sınırsız dijital arşiv</li>
        <li>✅ 1 çocuk</li>
        <li>✅ Yıllık albüm (500 foto)</li>
        <li>✅ Aile paylaşımı (3 kişi)</li>
      </ul>
      <button class="btn-secondary">Seç</button>
    </div>

    <div class="price-card featured">
      <div class="badge">Çoğu Aile</div>
      <h3>⭐ Premium</h3>
      <div class="price">₺1,999/yıl</div>
      <ul>
        <li>✅ Standart'taki her şey</li>
        <li>✅ 2 çocuk</li>
        <li>✅ Premium albüm (1000 foto)</li>
        <li>✅ Erken erişim özellikler</li>
      </ul>
      <button class="btn-primary">Seç</button>
    </div>

    <div class="price-card">
      <h3>VIP</h3>
      <div class="price">₺4,999/yıl</div>
      <ul>
        <li>✅ Premium'daki her şey</li>
        <li>✅ 3 çocuk</li>
        <li>✅ Özel tasarımcı</li>
        <li>✅ 24/7 destek</li>
      </ul>
      <button class="btn-secondary">Seç</button>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials">
  <h2>Kullanıcılar Ne Diyor?</h2>
  
  <div class="testimonial-grid">
    <div class="testimonial">
      <p>"İlk dişi kaybettimiz günü unutmayacağım. Vera sayesinde 3 yıl sonra hatırlattı. Ağladım."</p>
      <div class="author">- Elif, 28, İstanbul</div>
    </div>
    
    <div class="testimonial">
      <p>"Her yıl albüm alıyoruz. 8 yaşında 8 adet albüm verdik. Gözyaşları dökmeye başladı."</p>
      <div class="author">- Murat, 35, Ankara</div>
    </div>
  </div>
</section>

<!-- FAQ -->
<section class="faq" id="faq">
  <h2>Sıkça Sorulan Sorular</h2>
  
  <div class="faq-items">
    <details>
      <summary>Verilerim güvenli mi?</summary>
      <p>Evet. AES-256 encryption, daily backups, KVKK uyumlu. Verini istediğin zaman dışa aktarabilirsin.</p>
    </details>

    <details>
      <summary>Albüm ne zaman gelir?</summary>
      <p>Aralık sonunda (yıl sonu). Baskı ~10 gün, kargo ~3-5 gün. Yanı Yeni Yıl'da kolaylıkla gelir.</p>
    </details>

    <details>
      <summary>İptal edebilir miyim?</summary>
      <p>Evet, istediğin zaman. Ama albüm dayanağını kaybedersin (yönelik albüm siparişler iptal edilir).</p>
    </details>

    <details>
      <summary>Aile paylaşımı nasıl çalışır?</summary>
      <p>Babanne/babaanneyi davet edersin. Fotoğrafları görür, ama düzenleyemez. Her yıl albüm alabilir.</p>
    </details>

    <details>
      <summary>Fotoğraf limiti var mı?</summary>
      <p>Hayır. Sınırsız yükleme. Ama albümde max 500-1000 fotoğraf var.</p>
    </details>

    <details>
      <summary>İngilizce desteği var mı?</summary>
      <p>Henüz hayır (Türkçe only). 2026 Q3'de ekleyeceğiz.</p>
    </details>

    <details>
      <summary>Kime iletişim kurayım?</summary>
      <p>support@vera.app veya Instagram @veraapp</p>
    </details>
  </div>
</section>

<!-- FINAL CTA -->
<section class="final-cta">
  <h2>100 Aile Ücretsiz, Sonrası Normal Fiyat</h2>
  <p>Şimdi katıl, ilk yıl tamamen ücretsiz + ₺200 albüm kredisi kazan</p>
  <button class="cta-button-large" onclick="scrollToSignup()">
    ✨ HEMEN KATIL ✨
  </button>
</section>

<!-- EMAIL SIGNUP -->
<section class="email-signup" id="signup">
  <div class="signup-box">
    <h2>Beta'ya Katıl</h2>
    <p>E-posta adresi gir, liste'ye katıl. Beta başlayınca sana yazarız.</p>
    
    <form id="signupForm">
      <input type="email" placeholder="E-posta adresin..." required>
      <button type="submit">Beni Ekle ✨</button>
    </form>
    
    <p class="form-note">Spam yok. Sadece Vera haberleri. <a href="#">Privacy Policy</a></p>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-content">
    <div class="footer-links">
      <a href="#">Privacy Policy</a>
      <a href="#">Terms of Service</a>
      <a href="#">Contact</a>
    </div>
    
    <div class="footer-social">
      <a href="https://instagram.com/veraapp">Instagram</a>
      <a href="https://tiktok.com/@veraapp">TikTok</a>
    </div>
    
    <div class="footer-copyright">
      <p>&copy; 2026 Vera. Çocukların anılarını koruyor.</p>
    </div>
  </div>
</footer>

<script src="main.js"></script>
</body>
</html>
```

---

## CSS (Minimal, Performance-Focused)

```css
/* Global */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  line-height: 1.6;
  color: #333;
}

/* Hero */
.hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 80px 20px;
  text-align: center;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.hero h1 {
  font-size: 48px;
  margin-bottom: 20px;
  font-weight: 700;
}

.hero .subtitle {
  font-size: 20px;
  margin-bottom: 30px;
  opacity: 0.9;
}

.cta-button {
  background: #ff6b6b;
  color: white;
  border: none;
  padding: 16px 40px;
  font-size: 18px;
  border-radius: 50px;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

/* Grid */
.grid-3 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
  margin-top: 40px;
}

.card, .feature, .price-card {
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* Responsive */
@media (max-width: 768px) {
  .hero h1 { font-size: 32px; }
  .grid-3 { grid-template-columns: 1fr; }
}

@media (max-width: 480px) {
  .hero h1 { font-size: 24px; }
  .cta-button { padding: 12px 30px; font-size: 16px; }
}
```

---

## JavaScript (Form + Analytics)

```javascript
// Form handling
document.getElementById('signupForm')?.addEventListener('submit', async (e) => {
  e.preventDefault();
  
  const email = e.target.querySelector('input[type="email"]').value;
  
  // Send to GetResponse/Mailchimp
  const response = await fetch('/api/waitlist', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ email })
  });
  
  if (response.ok) {
    alert('✨ Listeye katıldın! Seninle yazarız.');
    e.target.reset();
  }
});

// Scroll to signup
function scrollToSignup() {
  document.getElementById('signup').scrollIntoView({ behavior: 'smooth' });
}

// Exit intent popup
document.addEventListener('mouseout', (e) => {
  if (e.clientY < 0) {
    showExitPopup();
  }
});

// Analytics (GA4)
window.dataLayer = window.dataLayer || [];
gtag('event', 'page_view');
gtag('event', 'cta_click', { section: 'hero' });
```

---

## Deployment

### Vercel (Recommended)

```bash
# Next.js version
npm create-next-app vera-landing

# Or simple HTML
# Just push to GitHub, Vercel auto-deploys
```

### Performance Targets

- ✅ Lighthouse: 95+ (Performance, SEO)
- ✅ Load time: <2 seconds
- ✅ Mobile: Fully responsive
- ✅ Mobile-first: Design for mobile FIRST
- ✅ Accessibility: WCAG AA

---

## What This Landing Page is NOT

❌ NO app preview/screenshots (use app for that)  
❌ NO technical jargon (emotional, not nerdy)  
❌ NO "download" button (web only)  
❌ NO newsletter signup for "tips" (only beta waitlist)  
❌ NO blog (not yet, focus on conversion)  

**Goal**: Get 100+ emails. That's it.

---

**Status**: 🟢 Ready to build
