# YASTIK ALTI — GİZLİLİK POLİTİKASI

**Yürürlük Tarihi:** 5 Mayıs 2026
**Son Güncelleme:** 5 Mayıs 2026
**Sürüm:** 1.1

---

## 1. GENEL HÜKÜMLER

### 1.1. Veri Sorumlusu
İşbu Gizlilik Politikası ("**Politika**"), **Yastık Altı** mobil uygulaması ("**Uygulama**") ile bağlantılı olarak kişisel verilerinizin nasıl toplandığını, işlendiğini, saklandığını, paylaşıldığını ve korunduğunu açıklamaktadır.

- **Veri Sorumlusu:** Doğan Cinek (gerçek kişi geliştirici), Türkiye Cumhuriyeti
- **İletişim:** devcinek@gmail.com
- **Uygulama:** Yastık Altı (App Store: com.dogancinek.yastikaltin)

### 1.2. Yasal Dayanak
İşbu Politika; **6698 sayılı Kişisel Verilerin Korunması Kanunu** ("**KVKK**"), **Avrupa Birliği Genel Veri Koruma Tüzüğü** ("**GDPR**") (geçerli olduğu ölçüde), **California Consumer Privacy Act / California Privacy Rights Act** ("**CCPA/CPRA**") (geçerli olduğu ölçüde) ve **Apple App Store Privacy Requirements** çerçevesinde hazırlanmıştır.

### 1.3. Politikanın Kabulü ve Bağlayıcılığı
Uygulamayı indirmeniz, kurmanız, açmanız veya herhangi bir şekilde kullanmanızla, işbu Politikada açıklanan veri işleme faaliyetlerini **okuduğunuzu, anladığınızı, eksiksiz biçimde kabul ettiğinizi ve bu işleme faaliyetlerine açık rıza verdiğinizi** kayıtsız şartsız beyan etmiş olursunuz. Politikayı kabul etmiyorsanız, Uygulamayı kullanmamak ve cihazınızdan kaldırmak yegâne çözüm yolunuzdur. Politikanın yorumlanmasında doğacak her türlü tereddüt, **kullanıcının lehine yorum kuralını dışlayacak şekilde**, Geliştiricinin makul ticari menfaatine ve işbu Politikanın amacına uygun olarak çözülür.

### 1.4. Kapsam
İşbu Politika; iOS uygulaması, Apple Watch eşlik uygulaması, ana ekran ve kilit ekranı widget'ları, Live Activity, Siri/App Intents, Multipeer Connectivity ve NearbyInteraction temelli "Altın Günü" özelliği, CloudKit özel veri tabanı senkronizasyonu, CloudKit Aile (paylaşılan) zone'u ve push bildirim altyapısı dahil olmak üzere Uygulamanın **tüm bileşenlerini** kapsar.

---

## 2. TOPLANAN VERİLER VE TOPLANMA YÖNTEMİ

### 2.1. **Cihazınızda Yerel Olarak Saklanan Veriler** (Geliştirici Sunucusuna Gönderilmez)

Aşağıdaki veriler **yalnızca cihazınızda** SwiftData/CoreData veritabanında ve App Group `UserDefaults` alanında saklanır; Geliştiricinin kontrolündeki **hiçbir sunucuya gönderilmez**:

| Veri Kategorisi | Detay |
|---|---|
| **Altın işlemleri** | Alım tarihi, gram miktarı, ödenen tutar (TRY/USD), kuyumcu adı (opsiyonel), notlar |
| **Gümüş işlemleri** | Aynı yapı; gümüş türü (Külçe/925/900/830/Gram), saflık katsayısı, işçilik delta'sı |
| **Finansal hedefler** | Hedef türü (gram/TL), hedef miktar, başlangıç/bitiş tarihi |
| **Kullanıcı tercihleri** | Bildirim eşik kuralları (yerel kopya), tema, dil, persona seçimi, kumbara hatırlatıcısı tarihi |
| **Widget veri kümesi** | Toplam gram, portföy değeri, gram fiyat, USD/TRY kuru — App Group içinde paylaşılır |
| **OCR/Fiş tarama (varsa)** | Fotoğraf, OCR çıkarımı sonrası **derhal cihazda silinir**; sadece kullanıcının kaydetmeyi seçtiği metin SwiftData kaydına geçer |

**Açıklama:** Bu veriler, kullanıcının iCloud yedeklemesi veya CloudKit senkronizasyonu açıksa Apple iCloud altyapısında saklanır (bkz. madde 2.5). Geliştiricinin bu verilere **hiçbir koşulda erişimi yoktur ve kuramaz**; SwiftData kayıtları cihaz/iCloud düzeyinde şifrelenir.

### 2.2. **Sunucu Tarafında Toplanan Veriler** (Sınırlı, Anonim veya Anonimleştirilmiş)

| Veri | Toplama Sebebi | Saklama Yeri | Saklama Süresi |
|---|---|---|---|
| **FCM Push Bildirim Token'ı** | iOS cihazınıza push bildirim gönderebilmek için Apple/Google tarafından üretilen anonim cihaz tanımlayıcısı | Firebase Cloud Messaging (Google Ireland Ltd.) + Google Sheets (sadece token) | Token geçerli olduğu sürece veya kullanıcı bildirim aboneliğini kapatana kadar |
| **Topic Abonelikleri** | `gold_daily`, `silver_daily`, `all_users` topic'lerine abonelik durumu (anonim) | Firebase Cloud Messaging | Aktif abonelik süresince |
| **Eşik Bildirim Tercihleri** | Fiyat/yüzde eşik kuralları (örn. "gram_gold > 4500 TL"); cihaz tanımlayıcısı yok, sadece anonim FCM token ile eşleşir | Google Sheets (Apps Script) | Kullanıcı silene kadar |
| **Live Activity APNs Token** | Dynamic Island ve Live Activity güncellemelerini APNs üzerinden push'lamak için Apple'ın ürettiği ephemerial token | Firebase Cloud Functions / Realtime Database (Google Ireland Ltd. veya ABD bölgesi) | Live Activity sona erdiğinde otomatik silinir; en geç **30 gün** içinde |
| **Live Activity Baseline Snapshot** | Push gönderiminde değişim yüzdesini hesaplamak için kayıt anındaki spot fiyat ve işçilik anlık değeri | Firebase Realtime Database | Aktivite sona erene kadar; en geç 30 gün |
| **Çökme Raporları** *(opsiyonel, varsa)* | Hata ayıklama için anonim çökme stack trace'leri; kişisel veri içermez | Apple App Store Connect veya muadili | 90 gün |

**Cihaz tanımlayıcısı (IDFA, IDFV) toplanmaz.** Reklam takibi yapılmaz. Geliştirici, bu sunucu kayıtlarından kullanıcının gerçek kimliğini geri çıkaracak hiçbir mekanizma çalıştırmaz.

### 2.3. **Apple Tarafından İşlenen Veriler** (Geliştirici Erişimi Yok)

App Store satın alma, abonelik yönetimi, iCloud, CloudKit ve APNs altyapıları çerçevesinde Apple aşağıdaki verileri kendi gizlilik politikası kapsamında işler. Geliştiricinin bu veriler üzerinde **kontrolü, görünürlüğü veya erişimi yoktur**:

- Apple Kimliği e-postası (Geliştiriciye **iletilmez**)
- Ödeme bilgileri (Geliştiriciye **iletilmez**, sadece "Premium aktif/pasif" durum bilgisi)
- StoreKit satın alma makbuzu (sadece doğrulama için)
- Cihaz modeli, iOS sürümü, App Store Connect analytics (anonim)
- iCloud / CloudKit kayıtları (Apple sunucularında, Apple ID'ye bağlı)
- APNs sertifika ve teslimat metadata'sı

### 2.4. **Toplanmayan Veri Kategorileri**

Aşağıdaki verileri **kesinlikle toplamıyoruz**:

- ❌ Ad, soyad, doğum tarihi, T.C. kimlik no
- ❌ E-posta adresi (siz bize doğrudan e-posta atmadıkça)
- ❌ Telefon numarası
- ❌ Açık adres, posta kodu
- ❌ Coğrafi konum (GPS, IP bazlı, Wi-Fi tabanlı)
- ❌ Mikrofon kaydı (Siri ifadeleri Apple'a gider; Geliştiriciye iletilmez)
- ❌ Fotoğraf galerisi (kullanıcı manuel seçim yapmadıkça)
- ❌ Rehber, takvim, sağlık verileri
- ❌ IDFA, IDFV
- ❌ Banka hesabı, kredi kartı bilgileri
- ❌ Şifre, biyometrik kimlik bilgileri
- ❌ Ses tonu / konuşma örneği / biyometrik ses imzası
- ❌ Üçüncü taraflara satılabilecek herhangi bir kişisel bilgi

### 2.5. **iCloud / CloudKit Özel (Private) Veri Tabanı Senkronizasyonu**

Uygulama, kullanıcının cihazları arasında işlemler ve hedeflerin senkronize edilmesi için **Apple CloudKit Private Database** altyapısını kullanır:

- Senkronizasyon **kullanıcının Apple ID'sine bağlıdır** ve **münhasıran Apple altyapısında** gerçekleşir;
- Geliştiricinin CloudKit Private DB içeriğine **erişimi yoktur ve teknik olarak da imkansızdır**;
- Senkronizasyonun aktif olabilmesi için kullanıcının iOS cihazında iCloud hesabının açık olması, "iCloud Drive" izninin verilmiş olması ve uygulama için iCloud erişiminin kapatılmamış olması gereklidir;
- Senkronizasyon hatalarından, gecikmelerinden, veri tutarsızlıklarından, çakışma çözümünde oluşan kayıplardan veya Apple'ın CloudKit hizmetinin kesintilerinden Geliştirici **sorumlu tutulamaz**;
- Senkronizasyonu kapatmak için: iOS Ayarlar → Apple Kimliğiniz → iCloud → Yastık Altı toggle'ı kapatın. Bu durumda yeni veriler bulut üzerine yazılmaz; mevcut bulut kayıtları Apple'ın iCloud silme politikasına tabidir.

### 2.6. **CloudKit Aile Portföyü (CKShare) — KRİTİK BİLDİRİM**

Uygulamanın "Aile Portföyü" özelliği, **Apple CloudKit Sharing** (CKShare) altyapısını kullanır. Kullanıcı (ev sahibi) bir paylaşılan zone oluşturup CKShare URL'si üzerinden başka kişileri (davetlileri) davet edebilir.

**Veri Akışı ve Görünürlük:**

| Görünür Olan | Kime Görünür | Kapsam |
|---|---|---|
| Paylaşılan zone'daki tüm işlem kayıtları | Davet eden + tüm kabul eden katılımcılar | Gram, ödenen tutar, kuyumcu, notlar dahil |
| Paylaşılan hedefler | Aynı | Hedef adı, tutar, ilerleme |
| Katılımcı görünen ad / Apple ID görünen e-postası | Davet eden + diğer katılımcılar | Apple'ın CKShare sistemi tarafından ortaya konur |

**Ortak Kontrolör (Joint Controller) Hükmü (KVKK / GDPR):**

Aile Portföyü oluşturan ev sahibi ve daveti kabul eden tüm katılımcılar, paylaşılan veriler bakımından **ortak veri kontrolörü** sıfatını haizdir. Geliştirici, Aile Portföyü içindeki paylaşımlardan, üçüncü taraf katılımcıların eylemlerinden, paylaşılan zone içindeki yanlış/yanıltıcı/hukuka aykırı veri girişlerinden veya katılımcılar arasındaki ihtilaflardan **hiçbir şekilde sorumlu tutulamaz**. Davet eden kullanıcı:

- Davet ettiği tüm katılımcıların **18 yaşının üstünde** olduğunu veya geçerli ebeveyn rızasına sahip olduğunu;
- Davet ettiği katılımcıların işbu Politikayı ve Kullanım Koşullarını kabul ettiklerini;
- Paylaşılan içerikte üçüncü tarafların kişisel verilerinin paylaşılmadığını veya paylaşılıyorsa ilgili kişilerin açık rızasının alındığını

**peşinen beyan, kabul ve taahhüt eder** ve bu beyanın aksinin ortaya çıkması halinde Geliştiriciyi tüm taleplere karşı **tazmin etmeyi** kabul eder (bkz. Kullanım Koşulları, Tazminat hükmü).

**Davetin İptali ve Veri Silme:**

- Ev sahibi household'ı silebilir; bu durumda CloudKit zone'u Apple tarafından silinir.
- Davetli, CKShare'i reddedebilir veya kabul ettikten sonra zone'dan ayrılabilir; ancak Apple'ın teknik kısıtları nedeniyle ev sahibi olmadan bir invitee tek başına zone'u silemez.
- Apple altyapısındaki gecikme ve eventual consistency davranışlarından Geliştirici sorumlu değildir.

### 2.7. **Apple Watch + WCSession**

Uygulamanın watchOS eşlik uygulaması (Yastık Altı Watch App) ve Watch Complications uzantısı, iPhone ile saat arasında veri akışını **yalnızca cihazlar arası yerel WatchConnectivity (WCSession) `applicationContext`** mekanizmasıyla sağlar:

- Senkronize edilen alanlar: gram fiyat, toplam portföy değeri, kâr/zarar yüzdesi, USD/TRY, ons fiyatları, işlem sayısı, son güncelleme zamanı.
- **Veri Apple/Geliştirici sunucusuna gönderilmez**; doğrudan saat ↔ telefon bluetooth/wifi yerel kanalı üzerinden iletilir.
- Saat üzerindeki cache (App Group `UserDefaults`) cihaz silindiğinde temizlenir.

### 2.8. **Live Activity Push Altyapısı**

Live Activity (Dynamic Island) güncellemeleri için kullanılan veri akışı:

1. iOS uygulaması, Apple'ın ürettiği **APNs Live Activity push token**'ını ([uploader sınıfı](Yastık%20Altı/Notifications/LiveActivityTokenUploader.swift)) Geliştiricinin Firebase Cloud Functions endpoint'ine HTTPS üzerinden gönderir.
2. Cloud Function token'ı Realtime Database'e baseline (kayıt anındaki spot fiyat snapshot'ı) ile birlikte kaydeder.
3. Periyodik (10 dakikada bir) zamanlanmış fonksiyon RTDB'den verileri okuyup APNs ES256 JWT ile push gönderir; başarısız token'lar (BadDeviceToken vb.) sessiz şekilde temizlenir.
4. Live Activity sona erdiğinde token unregister edilir; en geç **30 gün** içinde otomatik temizlenir.

Token Apple tarafından üretilmiş anonim bir tanımlayıcı olup tek başına kullanıcı kimliğine eşlenemez. Push gönderiminde ayrıca isim, e-posta, IP veya cihaz parmak izi iletilmez.

### 2.9. **Altın Günü — Multipeer Connectivity, NearbyInteraction, Local Network**

Uygulamanın "Altın Günü" özelliği, **fiziki olarak yan yana olan** kullanıcıların yüz yüze altın günü (Türk geleneksel altın biriktirme oturumu) gerçekleştirmesini dijitalleştirir. Bu özellik şu izinleri ve teknolojileri gerektirir:

- **Local Network (Yerel Ağ) İzni** — Aynı Wi-Fi ağındaki yakındaki cihazları Bonjour servisi ile keşfetmek;
- **NSNearbyInteractionUsageDescription (NI)** — UWB destekli cihazlarda yaklaştırma/mesafe ölçümü ile fiziki transferi onaylamak;
- **Multipeer Connectivity** — Apple'ın peer-to-peer protokolü; mesajlaşma ve oturum koordinasyonu için.

**Veri Akışı:**

- Oturum boyunca kullanıcının seçtiği **takma ad (nickname)**, rastgele atanmış **avatar emojisi**, **gram miktarı**, **işlem zamanı** ve **transfer durumu** sadece o oturumdaki diğer cihazlarla doğrudan paylaşılır.
- Hiçbir veri Geliştirici sunucusuna ya da Apple sunucularına gönderilmez (Apple, MPC trafiğini sadece relay edebilir).
- Oturum sona erdiğinde paylaşılan veriler her cihazın yerel state'inden temizlenir; oturum özet kartı (ekran görüntüsü) kullanıcının kendi galerisinde yer alabilir.
- NI ile ölçülen mesafe verisi cihazda kalır; herhangi bir tarafa iletilmez.

**Kullanıcı Sorumluluğu:** Altın Günü özelliğini kullanan tüm katılımcılar, oturum başlamadan önce işbu Politikayı ve Kullanım Koşullarını kabul etmiş sayılır. Oturumda paylaşılan içerikten ve katılımcılar arası fiziki altın değişiminden Geliştirici **kesinlikle sorumlu değildir**. Uygulamadaki "transfer tamamlandı" ifadesi yalnızca dijital UI bildirimidir; **fiziki altın el değiştirmesi tamamen kullanıcılar arasındaki konudur**.

### 2.10. **Siri / App Intents**

Uygulama, iOS Siri ve App Shortcuts altyapısı üzerinden sesli sorgu (örn. "Hey Siri, Yastık Altı gram altın") destekler. Bu özelliklerde:

- Kullanıcının ses kaydı **Apple'ın Siri altyapısı** tarafından işlenir; Geliştiriciye iletilmez (Apple Siri Privacy: https://www.apple.com/legal/privacy/data/tr/siri/).
- Intent çalıştığında uygulama, App Group içinde tutulan **anlık portföy/fiyat snapshot'ını** okur; herhangi bir ağ çağrısı yapmaz, hiçbir veri dışarıya gönderilmez.
- Sesli komutla işlem ekleme intent'i çalıştırıldığında veri yalnızca cihazdaki SwiftData / CloudKit altyapısına yazılır.

---

## 3. VERİLERİN İŞLENME AMAÇLARI VE HUKUKİ DAYANAKLARI

### 3.1. KVKK Madde 5 / GDPR Madde 6 Çerçevesinde Hukuki Dayanaklar

| Veri | İşleme Amacı | Hukuki Dayanak |
|---|---|---|
| Yerel işlem verileri | Portföy hesaplaması, raporlama | Sözleşmenin ifası (KVKK 5/2-c, GDPR 6/1-b) |
| CloudKit Private Sync | Kullanıcının kendi cihazları arası senkronizasyon | Sözleşmenin ifası + açık rıza (KVKK 5/1) |
| CKShare Aile Portföyü | Davetlilerle ortak zone üzerinden veri paylaşımı | Açık rıza + ortak kontrolör mutabakatı (KVKK 5/1, GDPR 6/1-a + 26) |
| Apple Watch WCSession | Saatte canlı veri görüntüleme | Sözleşmenin ifası (KVKK 5/2-c, GDPR 6/1-b) |
| Live Activity push token | Dynamic Island / Live Activity güncellemeleri | Açık rıza (KVKK 5/1, GDPR 6/1-a) |
| FCM token + topic + eşik | Push bildirim teslimi | Açık rıza (KVKK 5/1, GDPR 6/1-a) |
| Multipeer / NI verileri | P2P altın günü oturumu | Açık rıza (KVKK 5/1, GDPR 6/1-a) |
| Apple satın alma durumu | Premium özelliklerin aktivasyonu | Sözleşmenin ifası (KVKK 5/2-c, GDPR 6/1-b) |
| Çökme raporları | Hata ayıklama, ürün iyileştirme | Meşru menfaat (KVKK 5/2-f, GDPR 6/1-f) |

### 3.2. Otomatik Karar Verme ve Profilleme
Uygulama, **otomatik karar verme süreçleri kullanmaz** ve kullanıcı profilleme yapmaz. Sell/Buy advisor (RSI/SMA) modülü tarihi fiyatlardan deterministik teknik göstergeler hesaplar; bu göstergeler **kişisel öneri değil, kamuya açık piyasa istatistiklerinden türetilen genel bilgi** mahiyetindedir. Kullanıcı için aleyhe sonuç doğuran otomatik karar mekanizması **bulunmamaktadır**.

---

## 4. VERİ PAYLAŞIMI VE ÜÇÜNCÜ TARAFLAR

### 4.1. Üçüncü Taraf Hizmet Sağlayıcıları

| Hizmet | Sağlayıcı | İşlenen Veri | Bulunduğu Konum |
|---|---|---|---|
| **App Store Dağıtım & Ödeme** | Apple Inc. (ABD) | Apple Kimliği, satın alma makbuzu | Apple altyapısı, küresel |
| **iCloud + CloudKit Private/Shared DB** | Apple Inc. | Kullanıcı veri kayıtları (Apple ID'ye bağlı) | Apple altyapısı, küresel |
| **APNs (Live Activity dahil)** | Apple Inc. | APNs token, push payload (anonim baseline) | Apple altyapısı |
| **Push Bildirim** | Google Ireland Ltd. (Firebase Cloud Messaging) | Anonim FCM token | AB / ABD veri merkezleri |
| **Sunucu Mantığı (Apps Script)** | Google LLC | Token + eşik kuralları (anonim) | ABD |
| **Cloud Functions + Realtime DB** | Google LLC / Firebase | Live Activity token + baseline (anonim) | ABD veya Avrupa bölgeleri |
| **Piyasa Verileri** | Üçüncü taraf finansal API sağlayıcıları | Veri talep IP'si (anonim) | Çeşitli |
| **ABD TÜFE (FRED® API)** | U.S. Bureau of Labor Statistics, FRED® (Federal Reserve Bank of St. Louis) aracılığıyla | Sadece kamuya açık ekonomik gösterge çekilir; kişisel veri paylaşılmaz | ABD |

> **FRED® Atıf:** Uygulama, ABD enflasyon hesaplamalarında FRED® API'sini kullanır. FRED® ve FRED logosu Federal Reserve Bank of St. Louis'in tescilli markalarıdır. St. Louis Fed bu uygulamayı **onaylamamakta veya desteklememektedir**. Asıl veri kaynağı: U.S. Bureau of Labor Statistics (kamuya açık).

### 4.2. **Üçüncü Taraflara Veri Satışı / Reklam Paylaşımı: SIFIR**

> Geliştirici, kullanıcı verilerini **HİÇBİR ÜÇÜNCÜ TARAFA SATMAZ, KİRALAMAZ, PAYLAŞMAZ veya REKLAM AMACIYLA İŞLEMEZ**.

CCPA/CPRA kapsamındaki "satış" ve "paylaşım" tanımları dahil olmak üzere hiçbir kişisel veri ticari değer karşılığında üçüncü taraflarla paylaşılmaz. ATT (App Tracking Transparency) izni istenmez.

### 4.3. Yasal Yükümlülüklerden Kaynaklı Paylaşım
Geliştirici, yalnızca aşağıdaki hallerde verileri yetkili mercilerle paylaşır:

- Türkiye Cumhuriyeti mahkemeleri veya yetkili savcılıklarının yasal taleplerinin gereği;
- Suç gelirlerinin aklanmasının önlenmesi mevzuatı kapsamındaki bildirim yükümlülükleri;
- Kullanıcının veya üçüncü tarafların yaşamına/güvenliğine yönelik **acil ve somut** tehlikenin engellenmesi.

Geliştirici, gerekli olmadığı halde gönüllü hiçbir veri paylaşımı gerçekleştirmez ve **yargı kararı olmaksızın resmi olmayan kolluk taleplerini reddetme hakkını saklı tutar**.

### 4.4. Yurt Dışına Veri Aktarımı
Uygulama, Apple iCloud/CloudKit, Firebase, Google Apps Script ve App Store altyapıları üzerinden **yurt dışında (AB ve ABD)** veri merkezlerini kullanır. Bu aktarımlar:

- **GDPR** kapsamında: Standart Sözleşme Hükümleri (SCC) veya Apple/Google'ın sertifikalı uyum mekanizmaları altında gerçekleşir;
- **KVKK** kapsamında: Kullanıcının açık rızası ile veya KVKK Kurulu'nun yeterli koruma sağladığını ilan ettiği mekanizmalar üzerinden gerçekleşir.

Push bildirim aboneliğini, CloudKit senkronizasyonunu, Aile Portföyünü veya Live Activity'yi etkinleştirmenizle, ilgili anonim kayıt/token verilerinin yurt dışına aktarımına **açık ve sarih rıza** vermiş sayılırsınız. Bu rıza her zaman ilgili özelliği kapatarak geri çekilebilir; ancak geri çekme **geçmişe etkili değildir** ve halihazırda gerçekleşmiş işlemleri geçersiz kılmaz.

---

## 5. ÇOCUKLARIN GİZLİLİĞİ

Uygulama **13 yaşın altındaki çocuklara yönelik değildir** ve bilerek 13 yaşın altındaki kullanıcılardan veri toplanmaz.

- **COPPA Uyumu (ABD):** 13 yaşın altındaki bir çocuğun verilerini topladığımızı öğrenirsek, bu verileri **derhal sileriz**.
- **GDPR / KVKK Uyumu:** 16 yaşın altındaki kullanıcılar için ebeveyn/vasi rızası gereklidir.
- **Aile Portföyüne davet edilen bir küçük çocuğun iCloud Family Sharing düzenlemesi**, davet eden ev sahibinin sorumluluğundadır.
- Çocuğunuzun veri sağladığını düşünüyorsanız: **devcinek@gmail.com** adresine bildirin.

---

## 6. VERİLERİN SAKLANMA SÜRELERİ

| Veri Kategorisi | Saklama Süresi |
|---|---|
| Cihaz üzerindeki yerel veriler | Kullanıcı uygulamayı silene veya verileri manuel temizleyene kadar |
| iCloud / CloudKit kayıtları | Apple'ın iCloud silme politikasına tabi; kullanıcının iCloud'dan elden veya "Manage Storage" ekranından silmesi gerekir |
| CKShare paylaşılan zone | Ev sahibi household'ı silinceye kadar; davetli ayrıldığında erişimi kesilir, kayıtlar zone'da kalır |
| FCM Token | Token geçerli olduğu sürece veya kullanıcı bildirimleri kapatana kadar (en fazla 12 ay inaktiflik sonrası temizlenir) |
| Eşik kuralları | Kullanıcı silene kadar |
| Live Activity APNs token + baseline | Aktivite sona erince; en geç 30 gün |
| Multipeer / NI oturum verileri | Oturum kapanır kapanmaz cihaz hafızasından temizlenir; sunucuya hiç gitmez |
| Çökme raporları | 90 gün |
| Yasal yükümlülük gereği | İlgili mevzuatın gerektirdiği süre (örn. ticari defter saklama: 10 yıl) |

---

## 7. KULLANICI HAKLARI

### 7.1. KVKK Kapsamındaki Haklarınız (Madde 11)
Veri sahibi olarak Geliştiriciye başvurarak şu haklarınızı kullanabilirsiniz:

a) Kişisel verilerinizin **işlenip işlenmediğini öğrenme**;
b) İşlenmişse, buna ilişkin **bilgi talep etme**;
c) İşlenme amacını ve amacına uygun kullanılıp kullanılmadığını öğrenme;
ç) Yurt içinde veya yurt dışında aktarıldığı üçüncü kişileri öğrenme;
d) **Eksik/yanlış işlenmişse düzeltilmesini** isteme;
e) Yasal süreler bitiminde **silinmesini veya yok edilmesini** talep etme;
f) (d) ve (e) maddelerine göre yapılan işlemlerin verilerinin aktarıldığı üçüncü kişilere bildirilmesini isteme;
g) Otomatik sistemler ile analiz edilmesi sonucu aleyhe bir sonuç çıkmasına itiraz etme;
ğ) Hukuka aykırı işleme nedeniyle zarara uğramışsanız zararın **giderilmesini** talep etme.

### 7.2. GDPR Kapsamındaki Haklarınız
Eğer AB/EEA mukimi iseniz, ek olarak:

- **Erişim hakkı** (Madde 15)
- **Düzeltme hakkı** (Madde 16)
- **Silme hakkı / "Unutulma hakkı"** (Madde 17)
- **İşlemenin kısıtlanması hakkı** (Madde 18)
- **Veri taşınabilirliği hakkı** (Madde 20)
- **İtiraz hakkı** (Madde 21)
- **Otomatik karara tabi olmama hakkı** (Madde 22)
- **Denetim makamına şikâyet hakkı** (KVKK Kurumu için: kvkk.gov.tr)

### 7.3. CCPA/CPRA Kapsamındaki Haklarınız (Kalifornia mukimleri)
- Toplanan veri kategorilerini bilme hakkı;
- Kişisel verilerinizin silinmesini talep hakkı;
- "Kişisel verilerimi satmayın/paylaşmayın" hakkı (zaten bunlara dayanan paylaşım yapmıyoruz);
- Hassas kişisel verilerin sınırlandırılması hakkı;
- Bu hakları kullandığınız için ayrımcılığa uğramama hakkı.

### 7.4. Hak Kullanım Yöntemi ve Kimlik Doğrulaması
Tüm talepler için: **devcinek@gmail.com**

E-postanızda mutlaka şu bilgileri sağlamanız gerekir; aksi takdirde talep, yetersiz bilgi gerekçesiyle **reddedilebilir**:

- Talebin türü (erişim, silme, düzeltme vb.) ve hangi veri kategorisine ilişkin olduğu;
- **Kimlik doğrulaması:** cihaz FCM token'ınızın **son 6 hanesi** (Ayarlar → Hakkında → Diagnostics ekranından alabilirsiniz) **veya** App Store satın alma makbuzunuzun ekran görüntüsü;
- İletişim e-posta adresiniz.

Talebiniz **30 gün içinde** sonuçlandırılır. Talebin haksız, orantısız, tekrar eden veya kötüye kullanılır nitelikte olduğu hallerde KVKK Madde 13/2 ve GDPR Madde 12/5 kapsamında **makul ücret** talep edilebilir veya talep **reddedilebilir**.

### 7.5. Aile Portföyü Verilerine İlişkin Hak Sınırları
Aile Portföyü (CKShare) verileri için tek başına Geliştiriciye yapılan silme/düzeltme talepleri, paylaşılan zone'un Apple altyapısında olması ve ortak kontrolör niteliği nedeniyle **teknik olarak sınırlıdır**. İlgili veri için:

- Davetli, kendi katılımını sonlandırabilir (zone'dan çıkma);
- Ev sahibi, household'ın tamamını silerek tüm zone'u kaldırabilir;
- Geliştirici, Apple'ın CloudKit altyapısına müdahale edemez ve bu kapsamda silme talebi Apple'a yönlendirilmelidir.

---

## 8. VERİ GÜVENLİĞİ

### 8.1. Teknik Önlemler
- iOS işletim sisteminin sağladığı **Sandbox** ve **Data Protection** (Class A) mekanizmaları;
- Uygulama içi veriler iOS Keychain ve şifreli SwiftData/SQLite üzerinde tutulur;
- Sunucu iletişimi **HTTPS / TLS 1.2+** zorunludur;
- FCM token aktarımı, Firebase'in TLS şifreli kanalı üzerinden;
- Cloud Functions endpoint'leri yalnızca beklenen payload formatlarını kabul eder;
- APNs push'lar ES256 JWT ile imzalanır;
- Multipeer Connectivity oturumları Apple'ın MCEncryptionRequired moduyla şifrelenir;
- Apps Script erişim logları aktiftir.

### 8.2. İdari Önlemler
- Geliştirici dışında hiç kimsenin verilere erişimi yoktur;
- Tüm üçüncü taraf hizmet sağlayıcıları, kendi veri işleme sözleşmelerine (Apple DPA, Google DPA) tabidir.

### 8.3. Veri İhlali Bildirimi
Bir veri ihlali tespit edilmesi halinde:

- KVKK Madde 12/5 kapsamında **72 saat içinde** KVKK Kurumu'na bildirim yapılır;
- GDPR Madde 33 kapsamında, AB veri öznelerini etkiliyorsa, **72 saat içinde** ilgili denetim makamına bildirim yapılır;
- Etkilenen kullanıcılara, gecikmeksizin uygulama içi bildirim ve/veya basın açıklaması yoluyla duyurulur.

### 8.4. Mücbir Sebep
Apple iCloud/CloudKit, Firebase, Apple Watch eşleşmesi, APNs, Multipeer/NI altyapıları gibi üçüncü taraf bileşenlerinin kesintilerinden, hatalarından, veri kayıplarından, sızıntılarından veya bu altyapılara yönelik dış saldırılardan kaynaklı zararlardan Geliştirici **hiçbir surette sorumlu tutulamaz**. Söz konusu bileşenlerin kullanım koşulları ve gizlilik politikaları ilgili sağlayıcılar nezdinde geçerlidir.

---

## 9. ÇEREZ VE BENZERİ TEKNOLOJİLER

Mobil uygulama olduğu için **klasik web çerezi (cookie) kullanılmaz**. Aşağıdaki yerel saklama mekanizmaları kullanılır:

| Mekanizma | Amaç |
|---|---|
| `UserDefaults` | Uygulama tercihleri (slot seçimleri, bildirim toggle'ları, debug flag'leri) |
| `App Group UserDefaults` | Ana uygulama ↔ Widget ↔ Watch veri paylaşımı (`group.com.dogancinek.yastikaltin`) |
| `SwiftData` (CoreData üstü) | İşlem ve hedef kayıtları |
| `iOS Keychain` | (Varsa) hassas tercih verileri |
| `Bundle Resources` | Tarihsel fiyat verileri (statik), ses dosyaları |

---

## 10. APPLE ATT (App Tracking Transparency)

Uygulama, Apple'ın **App Tracking Transparency** çerçevesi kapsamında **kullanıcı takibi yapmaz**. ATT izin penceresi gösterilmez. IDFA toplanmaz.

App Store'daki "App Privacy" etiketleri:

- ✅ **Data Not Collected** — büyük ölçüde geçerli
- Toplanan: yalnızca **"Diagnostics → Crash Data"** (varsa, anonim) ve **"Identifiers → Device ID"** (FCM/APNs token, kullanıcıyla eşleştirilmez)

---

## 11. POLİTİKADA YAPILACAK DEĞİŞİKLİKLER

Geliştirici, işbu Politikayı zaman zaman güncelleme hakkını saklı tutar. Esaslı değişiklikler:

- Yürürlüğe girmeden **en az 7 gün önce** uygulama içi bildirim ile duyurulur;
- "Son Güncelleme" tarihi yenilenir;
- Materyal değişiklik gerektiren durumlarda (yeni veri kategorisi toplanması, veri paylaşılan üçüncü taraf eklenmesi vb.) **yeniden onay** istenebilir.

Yürürlük tarihinden sonra Uygulamayı kullanmaya devam etmeniz, güncellenmiş Politikayı **kabul ettiğiniz** anlamına gelir. Herhangi bir değişikliği kabul etmemeniz halinde, yegâne çareniz Uygulamayı kullanmayı bırakmaktır.

---

## 12. İLETİŞİM VE BAŞVURU

| Konu | İletişim |
|---|---|
| Veri sahibi hakları, KVKK/GDPR/CCPA talepleri | devcinek@gmail.com |
| Genel sorular, ürün desteği | devcinek@gmail.com |
| KVKK denetim makamı | Kişisel Verileri Koruma Kurumu — www.kvkk.gov.tr |
| GDPR denetim makamı | İkamet ettiğiniz AB üye devletinin Veri Koruma Otoritesi |

---

## 13. DİL VE YORUM KURALI

İşbu Politika Türkçe ve İngilizce olarak yayımlanmıştır. **Çelişki halinde Türkçe metin esastır**. İşbu Politikadaki terimlerin yorumlanmasında doğan tereddütler, **kullanıcının lehine yorum kuralının uygulanmasına imkan vermeyecek şekilde**, Geliştiricinin makul ticari menfaati ve Türkiye Cumhuriyeti hukukunun emredici hükümleri çerçevesinde çözümlenir; örnekleyici sayım ifadeleri ("dahil ancak bunlarla sınırlı değildir" gibi) sınırlı yorumlanamaz.

---

**İŞBU GİZLİLİK POLİTİKASINI KABUL ETTİĞİNİZİ BEYAN EDEREK, KİŞİSEL VERİLERİNİZİN BURADA AÇIKLANAN ŞEKİLDE İŞLENMESİNE AÇIK, ÖZGÜR İRADENİZLE VE BİLGİLENDİRİLMİŞ OLARAK RIZA VERMİŞ SAYILIRSINIZ.**
