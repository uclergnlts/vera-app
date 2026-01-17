# 📱 App İşleyişi & Kullanıcı Flow'ları

## 1. İlk Gelen Kullanıcı (Day 1)

### Onboarding Flow (5 dakika)

```
┌─────────────────────────────────────────────────────┐
│ SPLASH SCREEN                                       │
│ Vera Logo + Loading spinner                         │
│ (Check if user logged in)                           │
└─────────────────────────────────────────────────────┘
                    ↓
        ┌───────────────────────────┐
        │ Logged in?                │
        ├───────────────────────────┤
        │ Yes → Go to Home          │
        │ No  → Onboarding          │
        └───────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ WELCOME SLIDE 1                                     │
│ 📸 "Her Anınız Saklı Kalsın"                       │
│ Subtitle: Çocuğunuzun yolculuğunu fotoğraflarla   │
│           kaydedin, yıllık albüm alın             │
│                                                     │
│ [Next] →                                           │
└─────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ WELCOME SLIDE 2                                     │
│ 🎁 "Yıllık Fiziksel Albüm"                         │
│ Subtitle: Çocuğunuzun her yaş dönemi güzel         │
│           şekilde basılmış albümde yaşasın        │
│                                                     │
│ [Next] →                                           │
└─────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ WELCOME SLIDE 3                                     │
│ 👨‍👩‍👧 "Ailenizle Paylaşın"                         │
│ Subtitle: Büyükannelerin, komşuların hepsi         │
│           fotoğrafları görebilsin                  │
│                                                     │
│ [Başla] →                                          │
└─────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ SIGN UP SCREEN                                      │
│                                                     │
│ Email: [________________]                           │
│ Password: [________________]                        │
│ (Password check: Güçlü/Orta/Zayıf)                │
│                                                     │
│ Alternatif:                                        │
│ [Google ile kaydol] [Apple ile kaydol]            │
│                                                     │
│ Email onay linkini gönder                         │
│ (Giriş yapabilmek için gerekli)                   │
│                                                     │
│ Zaten hesabın var mı? [Giriş yap]                │
└─────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ EMAIL VERIFICATION                                  │
│                                                     │
│ ✉️ Emailine bir link gönderdik                     │
│ [example@gmail.com]                                │
│                                                     │
│ Link'e tıkla ve geri dön                           │
│ (iOS'te otomatik açılacak)                         │
│                                                     │
│ [Yeniden Gönder]                                  │
└─────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ PROFILE SETUP                                       │
│                                                     │
│ Senin Adın Nedir?                                  │
│ [________________]                                  │
│                                                     │
│ Şohret Fotoğrafı (Opsiyonel)                      │
│ [📷 Kameradan Çek / 🖼️ Galeriden Seç]           │
│                                                     │
│ [Devam Et]                                         │
└─────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ ADD FIRST CHILD                                     │
│                                                     │
│ İlk Çocuğun Kimdir?                               │
│                                                     │
│ Adı: [________________]                             │
│ Doğum Tarihi: [15 Ocak 2024] ▼                    │
│ Fotoğrafı: [📷 Kameradan / 🖼️ Galeri]            │
│                                                     │
│ [Profili Oluştur]                                 │
└─────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────┐
│ HOME SCREEN (İlk kez)                              │
│                                                     │
│ Hoş Geldin, Elif! 👋                              │
│                                                     │
│ 👧 Emma, 1 ay 2 gün                               │
│ 0 Fotoğraf henüz yok                              │
│                                                     │
│ [📸 İlk Fotoğrafını Yükle] ← Büyük CTA            │
│                                                     │
│ Ekranın Altı: Bottom Navigation                    │
│ 🏠 Home | 📸 Upload | 🎁 Album | 👥 Family | ⚙️ Settings
│                                                     │
└─────────────────────────────────────────────────────┘
```

**Toplam Zaman**: 2-3 dakika (tüm adımlar hızlı)

---

## 2. Günlük Kullanıcı Journey

### Senaryo A: Fotoğraf Yükleme

```
HOME SCREEN'den başla
(Emma: 1 ay 2 gün, 0 fotoğraf)
         ↓
    [📸 Upload]
         ↓
┌──────────────────────────────────┐
│ UPLOAD SCREEN                    │
│                                  │
│ 👧 Emma, 1 ay 2 gün             │
│ [Fotoğraf Ekle]                 │
│                                  │
│ Gallery açılır...               │
│ [İlk fotoğraf seçilir] ✓        │
│ [2. fotoğraf seçilir] ✓         │
│ [3. fotoğraf seçilir] ✓         │
│                                  │
│ 3 Fotoğraf Seçildi             │
│ [İleri]                         │
└──────────────────────────────────┘
         ↓
┌──────────────────────────────────┐
│ EDIT PHOTOS                      │
│ (Her fotoğrafı Crop/Rotate)     │
│                                  │
│ Fotoğraf 1/3:                   │
│ [Fotoğraf Preview]              │
│ [✏️ Döndür] [📐 Kırp]          │
│                                  │
│ ← [Geri] | [İleri] →            │
└──────────────────────────────────┘
         ↓
┌──────────────────────────────────┐
│ ADD CAPTIONS                     │
│ (Fotoğraf 1/3)                  │
│                                  │
│ Hikaye Ekle (Opsiyonel):        │
│ ┌──────────────────────────────┐ │
│ │ Emma ilk kez gülümsedi 💕   │ │
│ │ (200/500 karakter)          │ │
│ └──────────────────────────────┘ │
│                                  │
│ Etiketler Ekle:                 │
│ [Milestone: İlk Gülüş] ✓        │
│ [Yer: Ev]                       │
│                                  │
│ ← [Geri] | [İleri] →            │
└──────────────────────────────────┘
         ↓
┌──────────────────────────────────┐
│ UPLOADING...                     │
│ 📡 Fotoğraf 1/3... ████░░░░░░   │
│ 📡 Fotoğraf 2/3... ██████░░░░   │
│ 📡 Fotoğraf 3/3... ████████░░   │
│                                  │
│ (WiFi var: +50 KB/s hızlı)      │
│ (Mobil: +10 KB/s yavaş)         │
└──────────────────────────────────┘
         ↓
┌──────────────────────────────────┐
│ ✅ BAŞARILI!                    │
│                                  │
│ 3 Fotoğraf Başarıyla Yüklendi   │
│                                  │
│ Emma'nın Timeline'ında görebilsin│
│                                  │
│ 🎉 10 Fotoğraf Yükle Rozetini   │
│    Açarsın (Gamification)       │
│                                  │
│ [Emma'nın Timeline'ına Git]     │
└──────────────────────────────────┘
         ↓
HOME SCREEN'ye dön
Emma: 1 ay 2 gün, 3 Fotoğraf ✓
```

**Toplam Zaman**: 3-5 dakika (WiFi, boyut bağlı)

---

### Senaryo B: Timeline'da Fotoğrafları Keşfetme

```
HOME SCREEN → [Emma'nın adına tıkla]
         ↓
┌──────────────────────────────────────────┐
│ EMMA'S TIMELINE (Infinite Scroll)        │
│                                          │
│ Bugün: 1 ay 2 gün 👧                   │
│ ┌──────────────────────────────────────┐ │
│ │ 1 ay                                 │ │
│ │ ┌───┬───┬───┐                        │ │
│ │ │📸 │📸 │📸 │ 3 Fotoğraf            │ │
│ │ └───┴───┴───┘                        │ │
│ │ "Emma ilk kez gülümsedi 💕" ← Hikaye │ │
│ └──────────────────────────────────────┘ │
│                                          │
│ [Aşağıya Scroll...]                     │
│                                          │
│ ┌──────────────────────────────────────┐ │
│ │ 0 ay (Yeni Doğan)                    │ │
│ │ ┌───┬───┐                            │ │
│ │ │📸 │📸 │ 2 Fotoğraf                │ │
│ │ └───┴───┘                            │
│ │ Hastaneden çıkış 💚                 │ │
│ └──────────────────────────────────────┘ │
│                                          │
│ Aşağı Kaydır... (daha eski fotoğraflar) │
└──────────────────────────────────────────┘

Fotoğrafa Tıkla:
         ↓
┌──────────────────────────────────────────┐
│ PHOTO DETAIL SCREEN                      │
│                                          │
│ [← Geri]          [Üç Nokta: Menü]      │
│                                          │
│ ┌──────────────────────────────────────┐ │
│ │                                      │ │
│ │      [Tam Fotoğraf]                 │ │
│ │      (Swipen: Önceki/Sonraki)      │ │
│ │                                      │ │
│ └──────────────────────────────────────┘ │
│                                          │
│ Emma, 1 ay 2 gün                        │
│ 15 Kasım 2024                           │
│                                          │
│ Hikaye:                                  │
│ "Emma ilk kez gülümsedi 💕"            │
│ [✏️ Düzenle]                           │
│                                          │
│ Etiketler:                               │
│ [Milestone: İlk Gülüş] [Yer: Ev]      │
│ [+ Etiket Ekle]                        │
│                                          │
│ 🤍 Favorile [Sil]                       │
│                                          │
└──────────────────────────────────────────┘

Menü (⋮):
  ├── ✏️ Hikaye Düzenle
  ├── 📤 Paylaş (WhatsApp, Instagram)
  ├── 💾 Cihaza İndir
  ├── 🗑️ Sil (Onayla)
  └── 🔗 Aile Üyesine Paylaş
```

**Toplam Zaman**: 30 saniye - 5 dakika (ne kadar karışmak istiyorlarsa)

---

### Senaryo C: Memory Card Bildirimi (Emoşyonal)

```
USER'İN TELEFONUNDA PUSH BİLDİRİMİ GELDI:

┌────────────────────────────────┐
│ 🔔 Vera - 2 Sene Öncesine Bugün│
│                                │
│ "Emma 1 yaşında ilk adımını    │
│  attı 👣"                      │
│                                │
│ [Dokunun Açılsın]              │
└────────────────────────────────┘

TIKLADI:
         ↓
┌────────────────────────────────────────┐
│ MEMORY CARD (Full Screen)              │
│                                        │
│                                        │
│     [Eski Fotoğraf]                   │
│     (Emma 1 yaş, ilk adım)            │
│                                        │
│                                        │
│ "2 Yıl Öncesine Bugün" 💝             │
│ "Emma ilk adımını attı 👣"             │
│                                        │
│ [← Geri]          [Paya Çık] →        │
└────────────────────────────────────────┘

SHARE TIKLADI:
  ├── 💬 WhatsApp'ta Gönder
  ├── 📱 Instagram Story'de Paylaş
  ├── 👥 Aileme Mail
  └── 💝 Kendime Kaydet (Clipboard)
```

**Efekt**: 1 sene sonra, aynen bu tarihte 
yeni bir memory card gelecek: "3 Yıl Öncesine..."

---

## 3. Özel İşlemler

### Album Creation Flow (Yıl Sonunda)

```
Aralık 31, 2024 → USER'E NOTIFICATION:

┌────────────────────────────────┐
│ 🎁 Yıllık Albümün Hazır!      │
│                                │
│ Emma'nın 2024'ü kaydetme       │
│ zamanı geldi! (150 fotoğraf)   │
│                                │
│ [Albümü Özelleştir] →          │
└────────────────────────────────┘

ALBÜM ÖZELLEŞTIRME:
         ↓
┌────────────────────────────────────┐
│ EMMA'NİN 2024 ALBÜMÜ              │
│                                    │
│ Kullanılan Fotoğraf: 150/150      │
│ (AI'ın seçtiği en iyi 150)        │
│                                    │
│ [Auto] [Manual Seç] [Skip]        │
│                                    │
│ Tasarım Seç:                      │
│ ┌────────────────────────────────┐ │
│ │ 1️⃣ Modern (Minimalist)         │ │
│ │ 2️⃣ Klasik (Geleneksel)         │ │
│ │ 3️⃣ Sıcak (Aile-odaklı) ← Seç  │ │
│ │ 4️⃣ Oyuncu (Renkli)             │ │
│ │ 5️⃣ Şık (Premium)                │ │
│ └────────────────────────────────┘ │
│                                    │
│ Başlık Düzenle:                    │
│ [Emma'nın 2024'ü]                 │
│                                    │
│ Kapak Mesajı:                      │
│ [Yıl dolu mutluluk ve büyüme 💚] │
│                                    │
│ [PDF Önizlemesini Göster]         │
└────────────────────────────────────┘
         ↓
┌────────────────────────────────────┐
│ ALBÜM ÖNİZLEMESİ (PDF)            │
│                                    │
│ Sayfa: 1/40 (A5, 148×210mm)       │
│                                    │
│ [Kapak]                            │
│ Emma'nın 2024'ü                    │
│ Yıl dolu mutluluk ve büyüme 💚    │
│                                    │
│ [← Geri] | [İleri →]              │
│                                    │
│ [İndir] [Sipariş Ver]             │
└────────────────────────────────────┘
         ↓
┌────────────────────────────────────┐
│ ALBÜM SİPARİŞİ                    │
│                                    │
│ Emma'nın 2024 Albümü              │
│ 40 Sayfa, A5 Boyut                │
│ Tasarım: Sıcak                    │
│ Fiyat: ₺1,500                     │
│                                    │
│ Kargo Adresi:                      │
│ [Elif Yılmaz]                     │
│ [Ankara, Türkiye]                 │
│                                    │
│ Teslimat: 5-7 iş günü            │
│                                    │
│ Ödeme Yöntemi:                     │
│ [Stripe: Kredi Kartı]             │
│ [İyzico: Yerel]                   │
│                                    │
│ [Sipariş Ver] → Stripe Checkout   │
└────────────────────────────────────┘
         ↓
✅ SİPARİŞ BAŞARILI!
   (Tracking numarası gönder)
```

---

### Family Sharing Flow

```
USER: "Büyükanne'ye Emma'nın fotoğraflarını göstermek istiyorum"

Home Screen → [⚙️ Settings]
         ↓
[👥 Aile Yönetimi]
         ↓
┌────────────────────────────────────┐
│ AILE ÜYELERİ                       │
│                                    │
│ ✅ Sen (Sahip)                    │
│                                    │
│ Davettiler:                        │
│ ⏳ Mehmet (Baba) - Pending        │
│    [✓ Kabul Et] [✗ İptal]        │
│                                    │
│ [+ Aile Üyesi Davet Et]           │
└────────────────────────────────────┘
         ↓
┌────────────────────────────────────┐
│ DAVET GÖNDER                       │
│                                    │
│ Kişi Bilgisi:                      │
│ Adı: [Ayşe (Büyükanne)]           │
│ Email: [ayse@gmail.com]           │
│                                    │
│ İzinler:                           │
│ ☑️ Fotoğrafları Görüntüle         │
│ ☐ Fotoğraf Yükle                 │
│ ☐ Hikaye Düzenle                 │
│ ☐ Albümü Düzenle                 │
│                                    │
│ Geçerlilik:                        │
│ [Süresiz] ▼                       │
│                                    │
│ [Daveti Gönder]                   │
└────────────────────────────────────┘

AYŞE'NİN CIHAZINDA:
Email gelir → Link'e tıklar
         ↓
┌────────────────────────────────────┐
│ DAVET KABUL ET                     │
│                                    │
│ Elif seni Emma'nın fotoğraflarını  │
│ görmeye davet etti!                │
│                                    │
│ [Daveti Kabul Et] vs [İptal]     │
│                                    │
│ Hesap gerekli mi? (Opsiyonel)     │
│ [Hesap Oluştur] [Yalnız Görünt]  │
└────────────────────────────────────┘
         ↓
AYŞE GÖRÜYOR:

┌────────────────────────────────────┐
│ AYŞE'NİN TIMELINE VIEW             │
│ (Elif'in hesabında)                │
│                                    │
│ 👧 Emma, 1 ay 2 gün              │
│ (VIEWER MODE - RO)                 │
│                                    │
│ [Timeline gridini görebilir]      │
│ [Fotoğraf detaylarını görebilir]  │
│ [Ama düzenleyemez]                │
│                                    │
│ Eğer "Can Upload" izni varsa:     │
│ [+ Fotoğraf Ekle] → Kendi'nin     │
│                                    │
│ [Elif'e Mesaj Gönder]             │
└────────────────────────────────────┘
```

---

## 4. Ayarlar ve Profil Yönetimi

```
HOME SCREEN → [⚙️ Settings]
         ↓
┌────────────────────────────────────┐
│ AYARLAR                            │
│                                    │
│ 👤 PROFİL                         │
│ ├─ Profil Resmi: [Elif Yılmaz]   │
│ ├─ Email: elif@gmail.com          │
│ ├─ Parolamı Değiştir             │
│ └─ Profilimi Düzenle             │
│                                    │
│ 👧 ÇOCUKLARIM                     │
│ ├─ + Emma (1 ay)                 │
│ ├─ + Mert (3 aylar)              │
│ └─ [+ Yeni Çocuk Ekle]           │
│                                    │
│ 📲 ABONELİK                       │
│ ├─ Plan: Standard (₺1,999/yıl)   │
│ ├─ Yenileme: 15 Ocak 2025        │
│ ├─ [Plani Değiştir]              │
│ └─ [Aboneliği İptal Et]          │
│                                    │
│ 🔔 BİLDİRİMLER                    │
│ ├─ ☑️ Push Bildirimleri Aç       │
│ ├─ ☑️ Günlük "Geçmişe Bugün"     │
│ ├─ ☑️ Albüm Hazır Bildirimi      │
│ ├─ ☑️ Aile Daveti Bildirimi      │
│ └─ ☑️ Yardımcı İpuçları          │
│                                    │
│ 🔒 GIZLILIK ve GÜVENLIK           │
│ ├─ 👁️ Face ID ile Giriş          │
│ ├─ [Verilerimi Dışa Aktar]       │
│ ├─ [Hesabımı Sil] (⚠️)           │
│ └─ [Gizlilik Politikası]         │
│                                    │
│ 📞 YARDIM                         │
│ ├─ [Sıkça Sorulan Sorular]       │
│ ├─ [Destek Ekibine Ulaş]         │
│ └─ [Hakkında] (v1.0.0)           │
│                                    │
│ [Çıkış Yap]                       │
└────────────────────────────────────┘
```

---

## 5. Offline Mode İşleyişi

```
SENARYOLAR:

Senaryo 1: Offline Fotoğraf Yükleme
────────────────────────────────────
User: WiFi'siz trenin içinde
Action: Fotoğraf yüklemeye çalışır

System:
┌────────────────────────────────┐
│ ⚠️ İnternet Bağlantısı Yok     │
│                                │
│ Fotoğraf sırada bekleniyor    │
│ İnternet döndüğünde, otomatik │
│ yüklenecek.                   │
│                                │
│ [✓ Devam Et] [⟳ Şimdi Yükle]  │
└────────────────────────────────┘

WiFi'ye bağlandığında:
↓
System otomatik upload başlat
Status: "Yükleniyor... 3/5"


Senaryo 2: Offline Timeline Görüntüleme
────────────────────────────────────────
User: Son 30 gün fotoğrafları local'de cached

┌────────────────────────────────┐
│ TIMELINE (Offline Mode)        │
│                                │
│ ✅ Tüm eski fotoğraflar yüklenmiş
│ (Cihazda saklanıyor)           │
│                                │
│ 🔴 Yeni fotoğraflar: Eski 30 gün
│ (Daha yeni olanlar offline)    │
│                                │
│ [Online Durumu Kontrol]        │
└────────────────────────────────┘


Senaryo 3: Hikaye Düzenleme (Offline)
───────────────────────────────────────
User: Offline'da eski bir fotoğrafa hikaye ekler

System:
├─ Değişiklik Local DB'ye kaydedilir
├─ Status badge: "Senkronize Beklemede"
├─ Online olduğunda otomatik senkronize
└─ Server'de başarılı → Badge kaybolur
```

---

## 6. Notification Strategy

### Notification Türleri & Zamanlaması

```
📲 BAŞLICA BİLDİRİMLER:

1️⃣ REMINDER BİLDİRİMLERİ
   ├─ "Bu ay 20 fotoğraf yükseldim,
   │   devam etmek güzel olur!" (Haftalık)
   ├─ "Emma'nın bu ay doğum günü!
   │   Anılarını hazırlayabilir misin?" (30 gün öncesi)
   └─ Timing: Öğle saati (12:30 PM)


2️⃣ MEMORY CARDS (Duygusal)
   ├─ "2 Yıl Öncesine Bugün..."
   │   (Eski bir tarihten fotoğraf)
   ├─ "1 Sene Önce Bu Gün Emma ilk
   │   adımını attı" (Milestone replay)
   └─ Timing: Sabah (8:00 AM) / Akşam (6:00 PM)
      (Kullanıcının davranışına göre optimize)


3️⃣ SYSTEM BİLDİRİMLERİ
   ├─ "Albümün Hazırlandı! Sipariş et"
   ├─ "Ailene Davet Kabul Etti"
   ├─ "Yeni Fotoğraf Yüklendi"
   └─ Timing: Aciliyet var → Hemen


4️⃣ AILE BİLDİRİMLERİ
   ├─ "Büyükanne Ayşe 5 fotoğraf ekledi"
   ├─ "Baba Mehmet Emma'nın ilk dişini
   │   milestone olarak işaretledi"
   └─ Timing: 10 dakika gecikmeli (spam değil)


5️⃣ MOTIVATIONAL (Hafif Gamification)
   ├─ "🎉 50 Fotoğraf Yükseldim! Rozetini Açtın"
   ├─ "📈 Bu Ay 20 Fotoğraf Yükseldim,
   │   Ağustosta 35 oldu!" (Trend)
   └─ Timing: Hafta sonunda (Cuma akşam)
```

### Notification İzin Yönetimi

```
İlk kurulumda:
┌────────────────────────────────┐
│ Vera Bildirimleri Kullanmak    │
│ İstiyor                        │
│                                │
│ Dosya erişimi ve hatırlatıcılar│
│ için gerekli                   │
│                                │
│ [İzin Ver] [Sonra Sor]        │
└────────────────────────────────┘

Settings'te granular kontrol:
├─ ☑️ Tüm Bildirimleri Aç
├─ ☑️ Günlük "Geçmişe Bugün"
├─ ☑️ Albüm Hazır Bildirimi
├─ ☑️ Aile Daveti Bildirimi
├─ ☑️ Haftalık Motivasyon
└─ ☐ Kampanya Emailleri (Marketing opt-in)

Do Not Disturb Saatleri:
├─ Başlangıç: [22:00]
├─ Bitiş: [08:00]
└─ (Sistem bu saatlerde yalnızca URGENT bildirir)
```

---

## 7. Sync & Offline Architecture (Technical)

```
DATA SYNC FLOW:

Local Device (SQLite):
┌─────────────────────────────────┐
│ users_local                      │
│ children_local                   │
│ photos_local (thumbnails)        │
│ photos_upload_queue (pending)    │
│ photo_captions_queue (pending)   │
│ tags_local                       │
└─────────────────────────────────┘
         ↕️ (Bi-directional sync)
         ↓
Cloud Server (PostgreSQL):
┌─────────────────────────────────┐
│ users (canonical)                │
│ children (canonical)             │
│ photos (originals in S3)          │
│ photos_captions (canonical)      │
│ tags (canonical)                 │
└─────────────────────────────────┘

SYNC MECHANISM:

1. Online Detect:
   ├─ System checks internet every 5 sec
   ├─ If online → Trigger sync

2. Upload Queue Process:
   ├─ photos_upload_queue üstünde başla
   ├─ Her fotoğraf: Multipart upload (S3)
   ├─ Metadata: POST /photos/upload
   ├─ Success → Queue'den sil
   ├─ Error → Retry 3x (exponential backoff)
   └─ Fatal error → Alert user

3. Conflict Resolution:
   ├─ If offline edit + server change:
   ├─ Server wins (canonical source)
   ├─ Local changes overwritten
   ├─ User notified (1-time alert)
   └─ Rarely happens (offline window = 24h max)

4. Sync Indicator:
   ├─ Timeline'da: 🔄 "Senkronize Ediliyor..."
   ├─ Upload başında: 📡 "Yükleniyor..."
   ├─ Hazır: ✅ (badge kaybolur)
   └─ Error: ⚠️ (retry UI)
```

---

## 8. Günlük Cycle (Örnek User)

```
ELİF'İN GÜNÜ (Tipik Vera Kullanımı):

08:00 - SABAH
├─ Push notification gelir: 
│  "2 Yıl Öncesine Bugün: Emma 1 yaşında
│   ilk adımını attı 👣"
├─ Bildirimi tıklar → Memory Card açılır
├─ Fotoğrafı görüp hüzünlü gülümsüyor 💕
└─ WhatsApp'ta kız kardeşine paylaşır

10:30 - SABAH (Park'ta)
├─ Emma'nın ilk kaydırmayı yaptı 🎉
├─ 5 fotoğraf çeker
├─ Vera uygulamasını açar
├─ [📸 Upload] → Fotoğrafları seçer
├─ Hikaye ekler: "Emma'nın ilk kaydırması!"
├─ Milestone tag ekler: "Gross Motor"
└─ Upload başlatır (WiFi var, hızlı)

14:00 - ÖĞLEDEN SONRA (Ofis'te)
├─ Email gelir:
│  "Ayşe (Büyükanne) Emma'nın
│   fotoğraflarını görüntüledi!"
└─ 2 yıl önce Emma'nın ilk dişini 
   milestone olarak etiketlemiş, Ayşe şimdi
   kaç diş çıktığını sorabilir

18:30 - AKŞAM (Eve dönüş)
├─ Mehmet (eş) WhatsApp yapıyor:
│  "Park'taki fotoğraflar çok güzel!"
├─ (Aile paylaşımı sayesinde görmüş)
└─ Elif: "Büyükanne bile reaksyon verdi!"

21:00 - GECE
├─ Yataktan önce Vera açar
├─ Emma'nın timeline'ında 10 fotoğrafa bakar
├─ Her birine hikaye ve tag ekler:
│  - "Uyku saati ritual 🌙"
│  - "Bedtime routine" milestone
├─ 2 tane favorite işaretler ⭐
└─ Uyumaya gider (DoNotDisturb: 22:00-08:00)

---

HAFTALIK SUMMARY:

Pazartesi:  8 fotoğraf yükledi
Salı:       0 fotoğraf
Çarşamba:  12 fotoğraf
Perşembe:   3 fotoğraf
Cuma:       15 fotoğraf
Cumartesi: 20 fotoğraf (Park günü)
Pazar:     10 fotoğraf

💰 Haftalık Metric:
├─ 68 fotoğraf yüklendi
├─ 85% fotoğrafa hikaye eklendi
├─ 3 milestone etiketlendi
├─ Aile üyesi: 2 (Büyükanne + Baba)
├─ Timeline viewing: 14 gün
└─ Status: 💪 ENGAGED USER
```

---

## Sonuç: App İçinde Ne Oluyor?

### Temel İş Döngüsü:

```
UPLOAD → ORGANIZE → SHARE → ENJOY → PRESERVE

1. UPLOAD
   └─ Fotoğraf seç, hikaye ekle, etiket yap, yükle

2. ORGANIZE
   └─ Timeline'da göz at, favorile, arayarla

3. SHARE
   └─ Aileleriyle paylaş, WhatsApp/Instagram'a gönder

4. ENJOY
   └─ Memory cards, notification'larla duygusal keyfin

5. PRESERVE
   └─ Yıllık albüm otomatik oluştur, basılı olarak sakla
```

### App'ın Ana Değeri:

```
✅ Beyin: Tüm fotoğrafları organize, tarihle, etiketle
✅ Kalp: Anıları tekrar keşfet, duygusal bağ kur
✅ Elleri: Ailesiyle paylaş, ortak anılar yarat
✅ El: Fiziksel albümle sonsuzlaştır
```

---

Bu app akışında **ne değişmesini, ne eklenmesini, ya da ne çıkarılmasını** istiyorsun?

- Ekran sayısı?
- Feature kompleksitesi?
- Notification sıklığı?
- Pricing/subscription flow?
- Aile işbirliği düzeyi?

Söyle, detaylı konuşalım! 🎯
