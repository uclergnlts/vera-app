# 🖨️ Printer Logistics Planı

## Türkiye'de Lokal Baskı Stratejisi

### 1. Vendor Analizi & Seçim

#### Target Printeryler (Ankara/İstanbul)

| Matbaa | Konum | Kapasite | COGS (std) | Lead Time | Notlar |
|--------|-------|----------|-----------|-----------|--------|
| **Ofset Basım A.Ş.** | Ankara | 500/hafta | ₺160 | 10 gün | Sert kapak expertise |
| **Mega Print** | İstanbul | 1000/hafta | ₺145 | 7 gün | Scale potansiyeli |
| **Color&Co** | İzmir | 300/hafta | ₺175 | 14 gün | Premium seçeneği |

**Strateji**: Mega Print (primary, scale için) + Ofset Basım A.Ş. (backup, Ankara'da local)

---

### 2. Baskı Spesifikasyonları

#### Standart Albüm (Öncelik 1)

```
Spec:
├── Boyut: A4 (210x297mm)
├── Sayfa: 50 sayfa (100 taraf)
├── Kağıt: 250gsm matte (iç), 300gsm sert kapak
├── Cilt: Perfect binding (yapıştırmalı)
├── Baskı: Full color 4/4
├── Laminasyon: Parlak kapak
└── Paketleme: Beyaz kutuda, bubble wrap

Fiyat Tahlili:
├── Plate/Setup: ₺2,500 (ilk 100 unit'te)
├── Per Unit: ₺140-160
└── Toplu indirim: 500+ = ₺120/unit
```

#### Premium Albüm (V1.1)

```
Spec:
├── Sayfa: 100 sayfa
├── Kağıt: 300gsm matte (iç), deri kapak
├── Cilt: Dikiş cilt (profesyonel)
├── Ek: Bookmark, kutulu paketleme
└── Per Unit: ₺280-320
```

---

### 3. Üretim Takvimi (Yıllık Döngü)

```
2026 Örneği:

Ocak
├── Abonelik başlar
└── Fotoğraf yükleme başlar

...

Kasım (Baskı Hazırlığı)
├── 1-15: Albüm preview (user selection)
├── 15-20: Final design (AI/manual)
└── 20-30: Printer'a dosya gönder

Aralık (Baskı Sezonu)
├── 1-10: Baskı başla
├── 10-20: Baskı bitir
├── 20-25: Kargo şirketi teslim al
└── 25-31: Teslimat başla (Yeni Yıl)

Ocak (Yeni Yıl)
├── Tüm albümler teslimat tamamla
├── Yenileme hatırlatmaları gönder
└── Döngü başa dön
```

**Kritik**: Kasım-Aralık = pik sezon, printer kapasitesi önemli!

---

### 4. Kargo & Logistics

#### Partner Seçim

| Şirket | Hız | Türkiye Kapsamı | Fiyat (A4) | Integration |
|--------|-----|-----------------|-----------|------------|
| **Aras Kargo** | 3-5 gün | %100 | ₺35 | API available |
| **UPS Türkiye** | 2-3 gün | %100 | ₺55 | Premium |
| **Yurtiçi Kargo** | 4-6 gün | %100 | ₺32 | API available |

**Seçim**: Aras Kargo (balance: hız + fiyat + coverage)

#### Kargo Maliyeti

```
Standart Albüm:
├── Paket ağırlığı: 800g
├── Boyut: A4+margin
├── Aras Fiyat: ₺35/package
└── Y1 1000 unit = ₺35K

Premium Albüm:
├── Ağırlık: 1.5kg
├── Aras Fiyat: ₺50/package
└── Tahmini 300 unit = ₺15K

Toplam Yıl 1 Kargo: ~₺50K
```

---

### 5. Quality Assurance

#### Print QA Flow

```
1. Proof Checking (3 gün)
   └── First 10 units inspect

2. Batch Random Check (%)
   ├── 100-500 units: 5% check
   ├── 500-1000 units: 2% check
   └── 1000+ units: 1% check

3. Defect Management
   ├── Damage rate: <1%
   ├── Color mismatch: <0.5%
   ├── Replacement: Free + express
   └── Complaint deadline: 30 gün
```

#### Printer Contract Terms

```
- Payment: 50% advance, 50% on delivery
- Lead time guarantee: ±2 gün
- Quality SLA: 98%+ acceptable
- Defect rate: <1%
- Rush fee: +15% (emergensi case)
- Minimum order: 100 unit
```

---

### 6. Cost Breakdown (Yıl 1)

#### Per Unit Economics (Standart)

```
Baskı:          ₺150
Kargo:          ₺35
Packaging:      ₺10
QA/Handling:    ₺5
─────────────────────
TOPLAM COGS:    ₺200/unit

Fiyat:          ₺999/yıl
Gross Profit:   ₺799
Margin:         %80
```

**Note**: Şu anki projection (₺180 COGS) conservative estimate'e göre revise edildi.

---

### 7. Scaling Plan

#### Yıl 2+ Projection

```
Yıl 2: 5,000 kullanıcı
├── Standart: 3,500 unit/yıl
├── Premium: 1,500 unit/yıl
└── Capacity risk: Mega Print = 1000/hafta = 52,000/yıl → OK

Yıl 3: 15,000 kullanıcı
├── Standart: 10,500 unit/yıl
├── Premium: 4,500 unit/yıl
└── Capacity risk: Multiple printer needed
    ├── Mega Print primary
    ├── Ofset Basım backup
    └── + 1 yeni vendor needed
```

#### Multi-Vendor Strategy

```
Yıl 2-3:
├── Mega Print: 60%
├── Ofset Basım: 30%
├── Yeni vendor: 10% (test)

Benefit:
├── Capacity buffer
├── Price leverage
├── Geographic redundancy
└── Quality competition
```

---

### 8. Teknoloji Integration

#### Printer API Workflow

```
Backend Flow:

1. User finalize design (Nov 20)
   └── POST /api/albums/{id}/finalize

2. System generates PDF
   ├── Image compression (optimize)
   ├── Bleed marks addition
   ├── Font embedding
   └── Color profile (ISO Coated v2)

3. Batch creation (daily)
   ├── Group by printer
   └── Queue job

4. FTP upload to Printer
   ├── Folder: /vera_2026_batch_001
   ├── Files: PDFs + JSON metadata
   └── Notification email

5. Printer confirms
   ├── Webhook: batch_received
   └── System update status → "printing"

6. Kargo handoff
   ├── Printer provides tracking IDs
   ├── System creates shipment labels
   └── Webhook: batch_shipped

7. Customer notification
   ├── Email: "Albümün baskısı başladı"
   ├── SMS: Tracking number
   └── Push: "3 gün içinde gelecek"
```

---

### 9. Risk Mitigation

| Risk | Mitigation |
|------|-----------|
| Printer kapasitesi yetersiz | Multi-vendor, pre-contract |
| Defect rate yüksek | QA process, SLA kontrol |
| Kargo gecikmesi | Backup kuryeler, tracking |
| File corruption | Backup systems, redundancy |
| Supply chain disruption | 2+ printer, stock buffer |

---

### 10. Immediate Actions (Sonraki 2 Hafta)

- [ ] Mega Print, Ofset Basım A.Ş. ile görüşme (capacity, pricing)
- [ ] Sample print order (100 unit Standart albüm)
- [ ] Kargo contract negotiate (Aras with bulk discount)
- [ ] PDF template oluştur (design file to print ready)
- [ ] FTP setup (printer ile data transfer)
- [ ] Defect SLA writedocument

---

**Status**: 🚀 READY FOR EXECUTION
