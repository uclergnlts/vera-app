# 🔒 Security & KVKK Compliance Checklist

## Data Protection (GDPR + KVKK)

### KVKK (Kişisel Verileri Koruma Kanunu) Compliance

```
1. Data Processing Agreement (DPA)
   ☐ KVKK compliant DPA prepared
   ☐ Data processor agreement with AWS/providers
   ☐ Sub-processor list maintained
   ☐ Data transfer agreements (if outside Turkey)

2. User Rights
   ☐ Right to access: User can download their data (JSON export)
   ☐ Right to deletion: "Delete all my data" feature
   ☐ Right to portability: Export in standard format
   ☐ Withdrawal of consent: Can revoke at any time
   ☐ Data request process: <30 days turnaround

3. Data Collection
   ☐ Explicit consent: Checkbox for terms + privacy policy
   ☐ Purpose limitation: Only use data for specified purposes
   ☐ Minimization: Collect only necessary data
   ☐ Transparency: Clear privacy policy in Turkish
```

### Implementation Checklist

#### Authentication & Access

```
☐ Password security
  ├─ Min 8 chars, mixed case, numbers, symbols
  ├─ Bcrypt hashing (cost factor 12)
  ├─ Salt stored separately
  └─ No password recovery (email reset only)

☐ JWT tokens
  ├─ 24-hour expiry for access token
  ├─ 30-day expiry for refresh token
  ├─ HS256 signing with secret key
  └─ Revocation list for logout

☐ Firebase Auth
  ├─ Enable 2FA (TOTP)
  ├─ Password reset via email only
  ├─ Account lockout after 5 failed attempts
  └─ Session management: Max 30 days

☐ API authentication
  ├─ X-API-Key header (for mobile)
  ├─ Rate limiting: 100 requests/min per user
  └─ IP whitelisting (for backend services)
```

#### Data Encryption

```
☐ In transit
  ├─ HTTPS only (TLS 1.3)
  ├─ HSTS header: max-age=31536000
  ├─ Certificate pinning (mobile app)
  └─ No HTTP fallback

☐ At rest
  ├─ AES-256-GCM encryption for photo metadata
  ├─ AWS KMS for encryption keys
  ├─ Key rotation: Every 90 days
  └─ Database encryption: PostgreSQL native

☐ In memory
  ├─ No plaintext passwords stored
  ├─ Clear sensitive data after use
  └─ Secure random generation (crypto library)
```

#### Photo Storage Security

```
☐ S3 bucket security
  ├─ Bucket encryption: AES-256
  ├─ Versioning: Enabled
  ├─ Access control: Private (no public read)
  ├─ Bucket policy: Only authenticated users
  ├─ Server-side encryption: Enabled
  ├─ CORS: Restricted to vera.app domains
  └─ Logging: CloudTrail enabled

☐ Photo URLs
  ├─ Presigned URLs: 1-hour expiry
  ├─ User verification: Check ownership before serve
  ├─ Rate limiting: Per-photo access limits
  └─ Watermark metadata: Timestamp + user_id

☐ EXIF data
  ├─ GPS data: Encrypted separately
  ├─ Camera info: Non-sensitive, stored as-is
  └─ Timestamp: Stored securely
```

#### Database Security

```
☐ PostgreSQL hardening
  ├─ User isolation: Each user has own connection pool
  ├─ Row-level security (RLS): Enabled
  ├─ Prepared statements: All queries use parameterized
  ├─ SQL injection prevention: Input validation + escaping
  └─ Connection pooling: PgBouncer with 10 connections

☐ Backups
  ├─ Encryption: AES-256
  ├─ Retention: 30 days
  ├─ Off-site: Different AWS region
  ├─ Testing: Monthly restore tests
  └─ Isolation: No credentials in backup
```

#### API Security

```
☐ Input validation
  ├─ Schema validation: Zod/Joi on every endpoint
  ├─ File upload: Check MIME type + file size (50MB max)
  ├─ Email validation: RFC 5322 compliant
  └─ XSS prevention: HTML sanitization

☐ Output encoding
  ├─ JSON responses: Properly escaped
  ├─ HTML: DOMPurify for user-generated content
  └─ CSV export: Quoted fields to prevent injection

☐ CSRF protection
  ├─ SameSite cookies: Strict mode
  ├─ CSRF tokens: For state-changing requests
  └─ Origin validation: Check request origin

☐ Rate limiting
  ├─ Per IP: 1000 requests/hour
  ├─ Per user: 100 requests/min
  ├─ Per endpoint: Customize by sensitivity
  └─ Backoff: Exponential with jitter
```

#### Compliance Monitoring

```
☐ Logging & auditing
  ├─ Access logs: All API calls logged
  ├─ Auth logs: Login/logout events
  ├─ Data modification: Who changed what, when
  ├─ Admin actions: Separate audit trail
  └─ Retention: 6 months minimum

☐ Alerts & monitoring
  ├─ Suspicious login: Alert on unusual location/time
  ├─ Bulk operations: Alert on mass data export
  ├─ Failed attempts: Alert after 5 failures
  └─ Database changes: Alert on schema modification
```

---

## Privacy Policy & Terms of Service

### Privacy Policy (Turkish, KVKK Compliant)

```markdown
# Gizlilik Politikası

## 1. Hangi Veriler Toplarız?

- E-posta adresi, şifre (hash'lenmiş)
- Çocuk adı, doğum tarihi, profil fotoğrafı
- Yüklediğiniz fotoğraflar ve videolar
- Fotoğraf metaveri (EXIF tarih, GPS)
- Hikaye yazıları, etiketler
- Kullanım istatistikleri (anonim)

## 2. Verileriniz Nasıl Kullanılır?

- Hizmet sunmak (fotoğraf arşivi, albüm üretimi)
- Kişiselleştirme (yaş-bazlı timeline)
- İletişim (bildirimler, e-posta)
- Iyileştirme (kullanım analitikleri)

## 3. Veri Güvenliği

- AES-256 şifreleme (saklanan veri)
- HTTPS/TLS (aktarılan veri)
- AWS KMS (anahtar yönetimi)
- Günlük yedeklemeler

## 4. Veri Saklama

- Etkin kullanıcılar: Abonelik süresi + 30 gün
- Silinen hesaplar: 30 gün (geri yükleme için)
- Yedeklemeler: 30 gün
- Yasal istekler: Gerektiği kadar

## 5. Haklarınız

- Erişim: Verilerinizi indir (JSON)
- Düzeltme: Profil bilgisi güncelleyin
- Silme: "Hesabı sil" butonu
- Rıza geri çekme: Abonelik iptal et
- Taşınabilirlik: JSON export

## 6. Dış Paylaşım

Verileriniz paylaşılmaz, aşağıdakiler hariç:
- AWS (veri depolama, yedekleme)
- Stripe/İyzico (ödeme işleme)
- Mailchimp (e-posta gönderimi)
- Sentry (hata izleme)

## 7. İletişim

Gizlilik hakkında soru: privacy@vera.app
KVKK talebi: kvkk@vera.app

Son güncelleme: 17 Ocak 2026
```

### Terms of Service (Turkish)

```markdown
# Hizmet Şartları

## 1. Kullanım Hakları

- Vera aboneliğiniz kişisel, ailevizin kullanımı içindir
- Ticari amaçla kullanamaz, satamaz, paylaşamaz

## 2. İçeriğin Sahipliği

- Yüklediğiniz fotoğraflar size ait kalır
- Vera bunları albüm üretimi için kullanır
- Vera reklamda kullanamaz (izin almaksızın)

## 3. Yasaklı İçerik

Aşağıdakiler yasaktır:
- Çocuk istismarı görselleri
- Taciz, nefret söylemi
- Telif hakkı ihlali
- Spam, malware

İhlal durumunda: Hesap fesih + yasal işlem.

## 4. Sorumluluk Sınırlandırması

Vera:
- Veri kaybından sorumlu değildir (backup yapın)
- Hizmet kesintisinden sorumlu değildir (force majeure)
- Üçüncü taraf hataları (AWS, Stripe) için sorumlu değildir

## 5. Fiyatlandırma & Ödeme

- Fiyatlar değişebilir (30 gün önceden bildirim)
- Abonelik otomatik yenilenir
- İptal kolay (bir tıkla)
- Geri ödeme: İlk 14 gün (tam iade)

## 6. Hizmet Değişiklikleri

Vera,koşulsuz:
- Özellik ekleyebilir, kaldırabilir
- Albüm tasarımını değiştirebilir
- Hizmet şartlarını güncelleyebilir (30 gün önce bildir)

Önemli değişiklik: İptal hakkı.

## 7. Yasal Yargı

- Türkiye Cumhuriyet Kanunları
- Ankara Adli Tebliğ Mahkemesi
- Uyuşmazlık çözümü: Arabulucu, sonra mahkeme

## 8. İletişim

Şikâyet, kişisel veri talebi: support@vera.app
KVKK sorunu: kvkk@vera.app

Son güncelleme: 17 Ocak 2026
```

---

## Penetration Testing & Security Audit

### Pre-Launch (Before Q2 Public Launch)

```
Phase 1: Automated Scanning (March)
├─ OWASP ZAP scan (web & API)
├─ Snyk security scan (dependencies)
├─ SonarQube code quality
└─ Lighthouse security score (target: 95+)

Phase 2: Manual Penetration Test (March)
├─ Hire external security firm
├─ Test authentication bypass
├─ Test authorization bypass
├─ Test data injection
├─ Test file upload vulnerabilities
├─ Test API rate limiting
└─ Report remediation: All critical fixed

Phase 3: KVKK Audit (March)
├─ Data processing agreement review
├─ Privacy policy compliance check
├─ Consent mechanisms verified
├─ Data access procedures reviewed
└─ Deletion procedures tested
```

### Post-Launch Monitoring

```
Quarterly:
├─ Security patches (all dependencies)
├─ Access logs review (anomalies)
├─ Failed login analysis (brute force attempts)
└─ Unauthorized data access (any?)

Annually:
├─ Full penetration test (external)
├─ KVKK compliance re-audit
├─ Security training for team
└─ Incident response plan update
```

---

## Incident Response Plan

### Data Breach Protocol

```
1. DISCOVERY (When found)
   └─ Immediate: Stop data flow, preserve evidence

2. CONTAINMENT (0-2 hours)
   ├─ Isolate affected systems
   ├─ Determine scope (how many users, what data)
   └─ Activate incident response team

3. NOTIFICATION (2-4 hours)
   ├─ If >10 users affected: Notify via email + in-app
   ├─ KVKK notification: Within 72 hours
   └─ Public disclosure: If critical, transparent

4. REMEDIATION (4-24 hours)
   ├─ Fix vulnerability
   ├─ Reset affected passwords
   ├─ Deploy security patch
   └─ Verify fix (penetration test)

5. RECOVERY (24+ hours)
   ├─ Restore from clean backup
   ├─ Monitor for recurrence
   └─ Post-mortem analysis

6. COMMUNICATION
   └─ Regular updates to affected users
```

---

## Compliance Checklist

- [ ] KVKK DPA signed
- [ ] Privacy policy translated & reviewed by lawyer
- [ ] Terms of Service signed off
- [ ] Photo consent form (for family members)
- [ ] AWS data processing agreement
- [ ] Stripe PCI DSS compliance
- [ ] Penetration test: TBD (before launch)
- [ ] KVKK audit: TBD (before launch)

---

**Status**: ✅ Framework ready, implementation checklist prepared
