# 💰 Gelir Modeli

## Gelir Akışları

### 1. Ana Gelir: Yıllık Abonelik

| Paket | Fiyat (₺/yıl) | İçerik |
|-------|---------------|--------|
| Standart | 999 | Dijital arşiv + 1 standart albüm |
| Premium | 1,999 | Dijital arşiv + 1 premium albüm |
| VIP | 4,999 | Dijital + premium albüm + özel tasarım |

### 2. Ek Gelirler

| Ürün | Fiyat (₺) | Açıklama |
|------|-----------|----------|
| Ek Standart Albüm | 499 | Aynı yıl, farklı albüm |
| Ek Premium Albüm | 799 | Aynı yıl, farklı albüm |
| Ek Sayfa (10 adet) | 99 | Albüme ek sayfalar |
| Ek Çocuk Profili | 499/yıl | 2. ve sonraki çocuklar |
| Aile Üyesi Albüm Kopyası | 299 | Büyükanne/baba için kopya |

### 3. Gelecek Gelirler (Yıl 2+)

| Ürün | Fiyat | Açıklama |
|------|-------|----------|
| AI Hikaye Paketi | 299/yıl | Otomatik hikaye yazımı |
| Dijital Miras Paketi | 599/yıl | Uzun vadeli arşiv garantisi |
| 18. Yaş Özel Albüm | 1,999 | Tüm yılların derlemesi |
| Video Derleme | 399/yıl | Yıllık video timeline |

---

## Gelir Modeli Detayları

### Abonelik Mekaniği

```
Yıllık Döngü:

Ocak ─────────────────────────────── Aralık
  │                                      │
  └─ Abonelik başlar                     │
      └─ Dijital arşiv aktif             │
          └─ Fotoğraf yükleme başlar     │
              └─ Yıl boyunca birikiyor   │
                  └─ Kasım: Albüm preview│
                      └─ Aralık: Albüm basılır
                          └─ Ocak: Kargo & Yenileme
```

### Renewal Stratejisi

| Zaman | Aksiyon |
|-------|---------|
| Yıl ortası | Yarı yıl özeti e-posta |
| 2 ay önce | Albüm preview gösterimi |
| 1 ay önce | Yenileme hatırlatması |
| Yenileme | Otomatik (iptal kolay) |
| 1 hafta sonra | Yeni yıl başlangıç kutlaması |

### Churn Azaltma Mekanizmaları

1. **Data Lock-in**: Yılların verisi = değerli
2. **Albüm Beklentisi**: "Albümüm gelmedi" = iptal yok
3. **Aile Paylaşımı**: Büyükanne de bekliyor
4. **Uzun Vadeli Vizyon**: 18 yıl commitment

---

## Maliyet Yapısı

### Değişken Maliyetler (Per User/Year)

| Kalem | Standart | Premium |
|-------|----------|---------|
| Albüm Baskı | ₺180 | ₺350 |
| Kargo | ₺50 | ₺50 |
| Ödeme İşlem (%3) | ₺30 | ₺60 |
| Cloud Depolama | ₺24 | ₺24 |
| Support (orantılı) | ₺20 | ₺30 |
| **Toplam COGS** | **₺304** | **₺514** |

### Gross Margin

| Paket | Fiyat | COGS | Gross Profit | Margin |
|-------|-------|------|--------------|--------|
| Standart | ₺999 | ₺304 | ₺695 | **70%** |
| Premium | ₺1,999 | ₺514 | ₺1,485 | **74%** |
| VIP | ₺4,999 | ₺850 | ₺4,149 | **83%** |

### Sabit Maliyetler (Aylık)

| Kalem | Yıl 1 | Yıl 2 | Yıl 3 |
|-------|-------|-------|-------|
| Ekip (3→5→10) | ₺80K | ₺150K | ₺350K |
| Hosting/Infra | ₺20K | ₺40K | ₺80K |
| Marketing | ₺30K | ₺80K | ₺200K |
| Operasyon | ₺20K | ₺40K | ₺70K |
| **Toplam** | **₺150K** | **₺310K** | **₺700K** |

---

## Finansal Projeksiyonlar

### Yıl 1 Projeksiyonu

```
Kullanıcılar:
- Q1: 50 (beta)
- Q2: 150
- Q3: 350
- Q4: 450 (yeni) + yenileme
- Yıl sonu: 1,000 aktif

Gelir:
- ARPU: ₺1,200/yıl (mix)
- Gross Revenue: ₺1,200 x 1,000 = ₺1.2M
- Gross Margin: ₺840K (70%)

Giderler:
- Sabit: ₺150K x 12 = ₺1.8M
- Net: -₺960K (yatırım gerekli)
```

### 3 Yıllık Projeksiyon

| Metrik | Yıl 1 | Yıl 2 | Yıl 3 |
|--------|-------|-------|-------|
| Kullanıcı | 1,000 | 5,000 | 15,000 |
| ARPU | ₺1,200 | ₺1,400 | ₺1,600 |
| ARR | ₺1.2M | ₺7M | ₺24M |
| Gross Margin | ₺840K | ₺5M | ₺17M |
| Sabit Gider | ₺1.8M | ₺3.7M | ₺8.4M |
| Net Profit | -₺960K | +₺1.3M | +₺8.6M |
| Burn Rate | ₺80K/ay | Breakeven | Profitable |

---

## Unit Economics

### Standart Paket

```
Yıllık Değerler:
├── Revenue: ₺999
├── COGS: ₺304
├── Gross Profit: ₺695
│
├── CAC: ₺400
├── Gross Profit - CAC: ₺295 (Yıl 1)
│
├── Retention: 90%
├── Lifetime: 5 yıl
└── LTV: ₺695 x 5 = ₺3,475

LTV:CAC = 3,475 / 400 = 8.7:1 ✅
```

### Premium Paket

```
Yıllık Değerler:
├── Revenue: ₺1,999
├── COGS: ₺514
├── Gross Profit: ₺1,485
│
├── CAC: ₺600
├── Gross Profit - CAC: ₺885 (Yıl 1)
│
├── Retention: 92%
├── Lifetime: 6 yıl
└── LTV: ₺1,485 x 6 = ₺8,910

LTV:CAC = 8,910 / 600 = 14.9:1 ✅✅
```

---

## Yatırım İhtiyacı

### Pre-Seed (Yıl 1)

| Kalem | Miktar |
|-------|--------|
| Ürün Geliştirme | ₺500K |
| Operasyonel Giderler | ₺1.2M |
| Marketing | ₺300K |
| Buffer | ₺200K |
| **Toplam** | **₺2.2M (~$65K)** |

### Kullanım

```
12 Aylık Runway:
├── MVP Development: 3 ay
├── Beta Launch: 2 ay
├── Marketing ramp: 4 ay
├── First Album Delivery: 3 ay
└── Series A Ready
```
