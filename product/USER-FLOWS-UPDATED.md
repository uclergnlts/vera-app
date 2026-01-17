# 📱 App İşleyişi & Kullanıcı Flow'ları (6-Month Comprehensive App)

## 1. Navbar Tasarımı - Bottom Tab Navigation

### Temel Layout

```
┌────────────────────────────────────────────────────────────────┐
│ HOME SCREEN                                                     │
│ ┌────────────────────────────────────────────────────────────┐ │
│ │ Vera                                        ⚙️ Settings     │ │
│ │                                                             │ │
│ │ 👧 Emma, 1 ay 2 gün                                       │ │
│ │                                                             │ │
│ │ [Timeline Grid - Infinite Scroll]                         │ │
│ │ 📸 📸 📸 📸 📸                                             │ │
│ │ 📸 📸 📸 📸 📸                                             │ │
│ │                                                             │ │
│ │ [Aşağıya Scroll...]                                      │ │
│ └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│ ┌────────────────────────────────────────────────────────────┐ │
│ │ 🏠 Home  │  ➕  │ 🎁 Album │ 👥 Family │ ⚙️  │             │ │
│ │          │      │         │          │    │                │ │
│ │  Active  │ PRIMARY BUTTON │                                 │ │
│ │          │   (Quick Add)  │                                 │ │
│ └────────────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────────────┘
```

### 5 Tab Yapısı

```
TAB 1: 🏠 HOME
├─ Seçili çocuğun timeline'ı
├─ Infinite scroll
├─ Tarih-yaş gruplandırması
└─ Photo detail tap

TAB 2: ➕ QUICK ADD (Merkez, Highlight)
├─ Primary button, always accessible
├─ Photo upload screen açılır
├─ Tarih-yorum-tag hızlı entry
└─ En önemli feature

TAB 3: 🎁 ALBUM
├─ Yıllık albüm tasarımı
├─ Albüm customize
├─ Geçmiş albümler
└─ Print on demand

TAB 4: 👥 FAMILY
├─ Aile üyelerini yönet
├─ Paylaşım izinleri
├─ Shared timeline (collaborative)
└─ Aile bireyleri tarafından eklenen fotoğraflar

TAB 5: ⚙️ SETTINGS
├─ Profile, subscription
├─ Çocukları yönet
├─ Notification preferences
└─ Privacy & account
```

---

## 2. Hızlı Fotoğraf Yükleme Flow (+ Button)

```
BOTTOM NAVBAR'da [➕] TIKLADI
         ↓
┌───────────────────────────────────────────────────────┐
│ QUICK PHOTO UPLOAD                                    │
│                                                       │
│ 👧 Hangi çocuğa?                                     │
│ [Emma, 1 ay] ▼                                       │
│                                                       │
│ [📷 Kameradan]  [🖼️ Galeriden]                      │
│                                                       │
│ (Tek veya birden fazla seç)                         │
└───────────────────────────────────────────────────────┘

Galeriden seçti: 1 fotoğraf
         ↓
┌───────────────────────────────────────────────────────┐
│ PHOTO METADATA FORM (Single Screen)                   │
│                                                       │
│ [📸 Fotoğraf Preview]                                │
│                                                       │
│ Çekilme Tarihi:                                      │
│ [15 Kasım 2024] ▼                                    │
│ (EXIF'ten otomatik, editable)                       │
│                                                       │
│ Yorum (Opsiyonel):                                  │
│ ┌─────────────────────────────────────────────────┐  │
│ │ Emma ilk kez gülümsedi                       │  │
│ │ (200/500 karakter)                           │  │
│ └─────────────────────────────────────────────────┘  │
│                                                       │
│ Etiketler (Opsiyonel):                              │
│ [Ev] [Bahçe] [Gülüş] [+ Ekle]                      │
│                                                       │
│ [Yükle]                                             │
└───────────────────────────────────────────────────────┘
         ↓
┌───────────────────────────────────────────────────────┐
│ UPLOADING...                                          │
│ ████████████ 85%                                      │
│                                                       │
│ [Background'da devam et]                            │
└───────────────────────────────────────────────────────┘
         ↓
HOME SCREEN'ye dön
(Upload başarılı ✓ notification)

**Toplam Zaman**: 30 saniye - 2 dakika
**UX Avantajı**: Bottom nav'dan her zaman hızlı erişim, minimal steps (3 adım)
```

---

## 3. Home Screen - Timeline View

```
🏠 HOME TAB (Default Landing)
         ↓
┌───────────────────────────────────────────────────────┐
│ EMMA'S TIMELINE (Infinite Scroll)                     │
│                                                       │
│ Bugün: 1 ay 2 gün 👧                                │
│                                                       │
│ ┌───────────────────────────────────────────────────┐ │
│ │ 1 ay                                              │ │
│ │ ┌───┬───┬───┐                                     │ │
│ │ │📸 │📸 │📸 │ 3 Fotoğraf                         │ │
│ │ └───┴───┴───┘                                     │ │
│ │ "Emma ilk kez gülümsedi" ← Yorum                 │ │
│ └───────────────────────────────────────────────────┘ │
│                                                       │
│ [Aşağıya Scroll...]                                 │
│                                                       │
│ ┌───────────────────────────────────────────────────┐ │
│ │ 0 ay (Yeni Doğan)                                │ │
│ │ ┌───┬───┐                                         │ │
│ │ │📸 │📸 │ 2 Fotoğraf                             │ │
│ │ └───┴───┘                                         │ │
│ │ Hastaneden çıkış                                │ │
│ └───────────────────────────────────────────────────┘ │
│                                                       │
│ [Aşağıya Kaydır... (daha eski fotoğraflar)]        │
└───────────────────────────────────────────────────────┘

Fotoğrafa Tıkla:
         ↓
┌───────────────────────────────────────────────────────┐
│ PHOTO DETAIL SCREEN                                  │
│                                                       │
│ [← Geri]          [⋮ Menu]                          │
│                                                       │
│ ┌───────────────────────────────────────────────────┐ │
│ │                                                   │ │
│ │      [Tam Fotoğraf]                             │ │
│ │      (Swipe: Önceki/Sonraki)                   │ │
│ │                                                   │ │
│ └───────────────────────────────────────────────────┘ │
│                                                       │
│ Emma, 1 ay 2 gün                                    │
│ 15 Kasım 2024                                       │
│                                                       │
│ Yorum:                                              │
│ "Emma ilk kez gülümsedi"                           │
│ [✏️ Düzenle]                                       │
│                                                       │
│ Etiketler:                                          │
│ [Ev] [Gülüş] [+ Etiket Ekle]                      │
│                                                       │
│ ❤️ Favorile [Sil]                                   │
│                                                       │
└───────────────────────────────────────────────────────┘

Menu (⋮):
  ├── ✏️ Yorum Düzenle
  ├── 📤 Paylaş (WhatsApp, Instagram)
  ├── 💾 Cihaza İndir
  └── 🗑️ Sil (Onayla)
```

---

## 4. Family Tab - Collaborative Photo Sharing

```
BOTTOM NAVBAR → [👥 FAMILY]
         ↓
┌───────────────────────────────────────────────────────┐
│ FAMILY TAB                                            │
│                                                       │
│ 👧 Emma'nın Ailesi                                  │
│                                                       │
│ Aile Üyeleri:                                       │
│ ✅ Sen (Sahip)                                      │
│ ✅ Mehmet (Baba)                                    │
│ ✅ Ayşe (Büyükanne)                                 │
│ ⏳ Zeynep (Teyze) - Pending                         │
│                                                       │
│ Shared Timeline:                                     │
│ [Tüm aile tarafından eklenen                       │
│  fotoğraflar burada görünür]                       │
│                                                       │
│ [+ Aile Üyesi Davet Et]                            │
│                                                       │
│ [Aile Ayarları]                                    │
└───────────────────────────────────────────────────────┘
         ↓
[Shared Timeline'ı göster]
(Ayşe'nin eklediği fotoğraf: "Park'taki eğlenceli anlar")
         ↓

AILE ÜYESİ [➕] TIKLADI:
         ↓
┌───────────────────────────────────────────────────────┐
│ QUICK UPLOAD (Family Member)                        │
│                                                       │
│ Emma'nın Ailesi                                      │
│                                                       │
│ [📷 Kameradan]  [🖼️ Galeriden]                      │
│                                                       │
│ (Tarih + yorum aynı şekilde)                       │
│                                                       │
│ Kimler görsün?                                       │
│ [Emma's Family (Tüm üyeler)]                       │
│                                                       │
│ [Yükle]                                             │
└───────────────────────────────────────────────────────┘
         ↓
✅ Upload başarılı
   (Elif'e notification: "Ayşe foto ekledi")

**Key Point**: Family members = full photo uploaders
Same simple flow, shared collaborative timeline
```

---

## 5. Album Tab - Yearly Album Management

```
🎁 ALBUM TAB
         ↓
┌───────────────────────────────────────────────────────┐
│ EMMA'NIN ALBUMLERI                                    │
│                                                       │
│ 2024 Albümü                                         │
│ [Albüm Kapak Önizlemesi]                           │
│ 150 Fotoğraf seçildi                               │
│ [Özelleştir] [Sipariş Ver]                        │
│                                                       │
│ 2023 Albümü                                         │
│ [Tamamlandı - Basıldı]                             │
│ Sipariş: 5 Ocak 2024                               │
│ [Takip Et] [Yeniden Sipariş]                      │
│                                                       │
│ [Yeni Albüm Oluştur]                               │
└───────────────────────────────────────────────────────┘

[Özelleştir] Tıklandı:
         ↓
┌───────────────────────────────────────────────────────┐
│ ALBUM CUSTOMIZATION                                  │
│                                                       │
│ Kullanılan Fotoğraf: 150/150                        │
│ (AI'ın seçtiği en iyi 150)                          │
│                                                       │
│ [Auto Seç] [Manual Seç] [Skip]                     │
│                                                       │
│ Tasarım Seç:                                        │
│ ┌───────────────────────────────────────────────┐    │
│ │ 1️⃣ Modern (Minimalist)                         │    │
│ │ 2️⃣ Klasik (Geleneksel)                         │    │
│ │ 3️⃣ Sıcak (Aile-odaklı) ← Seçildi             │    │
│ │ 4️⃣ Oyuncu (Renkli)                             │    │
│ │ 5️⃣ Şık (Premium)                                │    │
│ └───────────────────────────────────────────────┘    │
│                                                       │
│ Başlık Düzenle:                                     │
│ [Emma'nın 2024'ü]                                  │
│                                                       │
│ Kapak Mesajı:                                       │
│ [Yıl dolu mutluluk ve büyüme]                     │
│                                                       │
│ [PDF Önizlemesini Göster]                         │
│ [Sipariş Ver]                                       │
└───────────────────────────────────────────────────────┘
         ↓
┌───────────────────────────────────────────────────────┐
│ ALBUM SİPARİŞİ                                       │
│                                                       │
│ Emma'nın 2024 Albümü                               │
│ 40 Sayfa, A5 Boyut                                 │
│ Tasarım: Sıcak                                      │
│ Fiyat: ₺1,500                                       │
│                                                       │
│ Kargo Adresi:                                       │
│ [Elif Yılmaz]                                       │
│ [Ankara, Türkiye]                                   │
│                                                       │
│ Teslimat: 5-7 iş günü                              │
│                                                       │
│ [Stripe: Kredi Kartı] [İyzico]                    │
│                                                       │
│ [Sipariş Ver] → Ödeme İşlemi                      │
└───────────────────────────────────────────────────────┘
         ↓
✅ SİPARİŞ BAŞARILI!
   (Tracking number email)
```

---

## 6. Settings Tab - Profile & Preferences

```
⚙️ SETTINGS TAB
         ↓
┌───────────────────────────────────────────────────────┐
│ AYARLAR                                               │
│                                                       │
│ 👤 PROFİL                                            │
│ ├─ Profil Resmi: [Elif Yılmaz]                      │
│ ├─ Email: elif@gmail.com                            │
│ ├─ Parolamı Değiştir                               │
│ └─ Profilimi Düzenle                               │
│                                                       │
│ 👧 ÇOCUKLARIM                                        │
│ ├─ Emma (1 ay)                                      │
│ ├─ Mert (3 ay)                                      │
│ └─ [+ Yeni Çocuk Ekle]                             │
│                                                       │
│ 📲 ABONELİK                                          │
│ ├─ Plan: Standard (₺1,999/yıl)                     │
│ ├─ Yenileme: 15 Ocak 2025                          │
│ ├─ [Plani Değiştir]                                │
│ └─ [Aboneliği İptal Et]                            │
│                                                       │
│ 🔔 BİLDİRİMLER                                       │
│ ├─ ☑️ Push Bildirimleri Aç                         │
│ ├─ ☑️ Upload Hatırlatıcısı (Haftalık)             │
│ ├─ ☑️ Albüm Hazır Bildirimi                       │
│ └─ ☑️ Aile Daveti Bildirimi                       │
│                                                       │
│ 🔒 GIZLILIK ve GÜVENLIK                             │
│ ├─ 👁️ Face ID ile Giriş                           │
│ ├─ [Verilerimi Dışa Aktar]                        │
│ └─ [Hesabımı Sil] (⚠️)                            │
│                                                       │
│ 📞 YARDIM                                            │
│ ├─ [Sıkça Sorulan Sorular]                         │
│ ├─ [Destek Ekibine Ulaş]                           │
│ └─ [Hakkında] (v1.0.0)                             │
│                                                       │
│ [Çıkış Yap]                                         │
└───────────────────────────────────────────────────────┘
```

---

## 7. Tipik Bir Günün Cycle (Elif Örneği)

```
SABAH - 08:00
├─ App açar, Emma'nın timeline'ı görsün
├─ Önceki gün eklediği fotoğraflar gözden geçir
└─ 2 dakika

ÖĞLE - 12:30 (Park'ta)
├─ Emma'nın oyun oynadığı fotoğraf çeker (5 adet)
├─ Navbar'ın [➕] tıklar
├─ 5 fotoğraf seçer
├─ Tarih (otomatik), 1 yorum yazıyor
├─ Etiket ekleme opsiyonel geçiyor
├─ Yükle tıklar (WiFi, 1 dakika)
└─ 5 dakika total

AKŞAM - 18:00
├─ Family tab'ı açar
├─ Büyükanne Ayşe'nin 3 fotoğraf eklediğini görür
├─ Shared timeline'da göz atar
└─ 3 dakika

GECE - 21:00 (Yataktan önce)
├─ Home tab'ı açar
├─ Emma'nın timeline'ında fotoğraflara bakar
├─ 1-2 fotoğrafa yorum ekler (edit)
├─ 2 tanesini favorite işaretler ⭐
└─ 5-10 dakika

---

HAFTALIK SUMMARY:

Pazartesi:  8 fotoğraf yükledi
Salı:       0 fotoğraf
Çarşamba:  12 fotoğraf
Perşembe:   3 fotoğraf
Cuma:       15 fotoğraf
Cumartesi: 20 fotoğraf (Park günü)
Pazar:     10 fotoğraf

💪 HAFTALIK METRIC:
├─ 68 fotoğraf yüklendi
├─ 80% fotoğrafa yorum eklendi
├─ Aile üyesi: 3 (Baba + Büyükanne + Teyze)
├─ 3 aile üyesi de foto yüklediler (collaborative)
├─ Timeline viewing: 12-14 gün
└─ Status: ENGAGED USER
```

---

## 8. Temel İş Döngüsü

```
📱 APP'IN TEMEL AKIŞI:

UPLOAD (5 dakika)
├─ [➕] tap
├─ Photo seç
├─ Tarih + yorum
└─ Yükle

ORGANIZE (Opsiyonel - 3 dakika)
├─ Timeline'ı göz at
├─ Favorile
├─ Yorum ekle/düzenle
└─ Etiket ekle

COLLABORATE (Aile feature)
├─ Family tab
├─ Aile üyelerine davet gönder
├─ Shared timeline'ı incele
└─ Aile fotoğraflarını görsün

PRESERVE (Yıl sonunda - 10 dakika)
├─ Album tab → Customize
├─ Tasarım seç, başlık düzenle
├─ Sipariş ver
└─ 5-7 iş günü sonra albüm elinde

SHARE (Her zaman)
├─ Photo detail → Menu
├─ WhatsApp/Instagram seç
└─ Paylaş

---

APP'IN TEMEL DEĞERİ:

✅ Beyin: Tüm fotoğrafları organize, tarihle, etiketle
✅ El: Ailenizle paylaş, ortak anılar yaratın
✅ Kalp: Fiziksel albümle sonsuzlaştırın
✅ Professional: Clean, fast, no emotional manipulation
```

---

## 9. Key Design Decisions (6-Month Comprehensive App)

```
1. ✅ NAVBAR DESIGN
   ├─ 5 tab (Home, +Add, Album, Family, Settings)
   ├─ + button merkeze ve prominent
   └─ Bottom nav'dan her zaman hızlı erişim

2. ✅ QUICK UPLOAD (3-Step)
   ├─ Child seç → Photo seç → Date+Comment+Tags
   ├─ Tarih EXIF'ten otomatik
   ├─ Comment opsiyonel (duygu pornosu yok)
   └─ Tags opsiyonel

3. ✅ FAMILY COLLABORATION
   ├─ Diğer aile üyeleri FULL upload yetkisi
   ├─ Shared timeline (everyone sees)
   ├─ Notification: "Ayşe foto ekledi"
   └─ Same simple UX for family

4. ✅ PROFESSIONAL TONE
   ├─ Duygu pornosu değil (Memory cards removed)
   ├─ Clean, minimal UI
   ├─ Practical notifications (upload reminders)
   └─ Focus: organize, preserve, share

5. ✅ 6-MONTH TIMELINE
   ├─ Jan-Mar: Core features (upload, timeline, album, family)
   ├─ Apr-Jun: Advanced (search, tags, integrations, analytics)
   └─ NOT MVP - comprehensive, full-featured app
```

---

**Status**: ✅ Complete user flows with 5-tab navigation, quick upload, family collaboration
