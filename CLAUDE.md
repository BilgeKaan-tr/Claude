# PSYCHE — Proje Brifingi

> Bu projeyi devralırsan **önce bu dosyayı**, sonra `psyche_mvp.html`'i oku. Geri kalan tasarım dokümanları (v0.3 tasarım notu, kart katalogu vb.) **referans amaçlıdır, eylemi yönlendirmez** — kararların güncel hâli aşağıda. Çelişki çıkarsa, **CLAUDE.md kazanır.**

---

## Oyun nedir

PSYCHE, kamuflaj stratejili psikolojik bir deckbuilder roguelite. İlk ~3 saat sıradan bir Slay the Spire benzeri olarak okunur (**Faz 0**). Sonra çatlaklar açılır ve oyunun aslında ölmekte olan bir beynin son halüsinasyonu olduğu yavaşça ortaya çıkar. Strateji: **Inscryption metodu** — bait-and-switch. Numaranın çalışması için açılış **gerçekten** sıradan olmalı; gizlenen sanat tarzı değil, **anlatı gerçeği**dir.

---

## Geliştirici / cihaz kısıtı

- Yazar: tek kişi, kod yazmıyor, psikoloji öğrencisi.
- Cihaz: tablet + Bluetooth klavye + mouse. PC yok.
- Yöntem: AI tüm kodu yazar; kullanıcı tabletinde oynar ve yön verir.
- Mecra: tarayıcıda çalışan vanilya HTML/JS (kütüphane yok). Web bir **tavan değil malzemedir** — Electron/NW.js ile Steam'e, Capacitor ile mobile paketlenebilir.

---

## Mevcut durum — kanıtlanmış olan

- Tek dosya: `psyche_mvp.html`.
- **Mini-PSYCHE prototipi:** 5 dövüş, 4 düşman arketipi (Bastırma Yumağı, İnkar Kabuğu, Kaygı Sarmalı, Şüphe, Yas), dövüş arası 3'ten 1 kart ödülü, dövüş arası +5 iyileşme.
- 14 kartlık Psikanalist Faz 0 destesi (`STARTER`) + 7 kartlık ödül havuzu (`REWARD_POOL`).
- Tüm kartlar `CARDS` objesinde, düşmanlar `ENEMIES` dizisinde — **veri odaklı**, mimariye dokunmadan denge ayarlanabilir.
- Statüsler: `telkin` (sonraki saldırıya +X), `zayıflık` (saldırı -%33), `ruya` (gecikmeli hasar), `block` (zırh).
- Pasif: **Gizli Kart** — savaş başı 1 kart kapalı belirir, oynandığında açılır.

**Doğrulanmış kullanıcı geri bildirimi:**
- "Su gibi akıp gitti" → çekirdek döngü tekrarda tutuyor (A ekseni testi geçti).
- "Biraz daha zorlu olabilir, düşündürücü olmalı" → mevcut sürüm bu nota göre sertleştirildi: düşman HP+, hasar+, Şüphe Zayıflığı %25→%33, dövüş arası iyileşme 10→5, Yas büyük vuruş 20→24.

---

## KİLİTLİ kararlar — yeniden açma

### 1. Okunabilirlik kuralı (Faz 0 yerleştirme testi)

Her unsur için sor: *"Tür-okur bir oyuncu bunu 'normal SLS mekaniği' olarak mı okur, yoksa 'bu aslında psikoloji/ölüm hakkında' diye mi bağırır?"*

- Birincisi → **Yüzey** (Faz 0'da olur).
- İkincisi → **Derin** (çatlaktan sonra gelir).

Bu kural her tasarım kararını filtreler. Eski tasarım dokümanlarındaki "her dövüşte ahlaki seçim", "klinik kart isimleri", "ölüm temalı UI" gibi unsurlar BU KURALDAN ÇAKAR ve geciktirilmiştir.

### 2. Çözümleme = ilk çatlak (silinmedi, geciktirildi)

Eski tasarım: her düşman öldüğünde KABUL ET / BASTIR / DÖNÜŞTÜR seçimi. **Güncel karar:** Faz 0'da düşmanlar normal ölür. Çözümleme'nin ilk açılması, kamuflajın **ilk çatlağı** olur — mekanik = tema. Faz 0 prototipine **eklenmeyecek**.

### 3. Kart kataloğu kaderi (v1.0 raflandı)

`psyche_kart_katalogu (1).docx`'teki ~80 kartlık v1.0 havuzu **Bastırma Sayacı** motoru üstüne kurulu — bu motor Faz 0 için fazla gürültülü. O kartların büyük çoğunluğu **silinmedi, raflandı**: reveal-sonrası havuz olarak yaşar; çatlakla birlikte destenin kimliği kayar (bonus drip-feed). Faz 0 destesi sıfırdan yazıldı.

### 4. Pasif sürümleri (iki katmanlı tasarım)

- **Faz 0 Psikanalist pasifi:** sade **Gizli Kart** (savaş başı 1 kart kapalı). Defect orb'u gibi okunur, kimseyi şüphelendirmez.
- **v1.0 Bastırma Sayacı + 5'te patlama:** Faz 2+ evrimi (oyuncu reveal sonrası buna yükselir). Şimdilik kodda yok.

### 5. Web mecrasının amacı

Web prototipi oyuncak değildir; **doğrulama + gösterim**dir. Eğlenceli olduğu kanıtlandığında ya HTML5 paketlenir (Electron → Steam), ya da motor portu için sağlam bir şartname olur. **Erken motor seçimi (Godot dahil) kaçıştır** — döngü kanıtlanmadan motor değişmez.

---

## YAPMAYACAKLAR (önemli)

- Faz 0 prototipine reveal mekaniği, anomali, niyet yalanı, Çözümleme ekranı, dördüncü duvar kırılması, klinik dil **ekleme**. Bunlar Faz 1+ malzemesi.
- Sanatsal cila, görseller, ses, müzik, parçacık efektleri **ekleme** — döngü yıpranmaya karşı dayanıklı görülmeden önce. Greybox kalsın.
- Kapsam genişletme: 136 kart, 3 karakter, Cardiac Audio System, ilişki sistemi vb. Tasarım dokümanlarında yazılı her şey Faz 1+ ya da daha sonra.
- Yeni motor/araç önerme. Tek dosya HTML'i savun; çok dosyaya bölme ihtiyacı **gerçekten** doğana kadar bekle.

---

## Sıradaki gerçek iş (önceliklendirilmiş)

1. **Mevcut zorluk sürümünü doğrula:** Kullanıcı sert sürümü oynamalı. Yargı şu eksende beklenir: *"dişli akış"* (düşündürür ama akar — istenen) vs *"takılı sinir bozucu"* (geri çekme gerekir).
2. **Sayı ayarı (cevaba göre):** Tek tek düşman/kart/iyileşme değerleri. Mimari değil, sayı.
3. **Yol seçimi:** 5 dövüşlük doğrusal parkur → küçük harita ağacı (her düğümde 2 seçenek). A ekseninin son testi: oyuncu *agency* hissediyor mu?
4. **Sonra (ve sadece sonra):** İlk çatlak — tek bir niyet-yalanı ya da Çözümleme'nin ilk açılması. Mimaride ayrı bir "Faz 1 giriş noktası".

---

## Tasarımcı profili (handoff iletişim notu)

Yeni oturum, bu kişiyle nasıl konuşacağını bilmiyor — bu yüzden yazıyorum:

- Psikoloji öğrencisi, kod bilmiyor; kararları sezgisel + analitik veriyor. Detay takıntılı, tümdengelimsel düşünür.
- **Reddediliyor:** Söze giriş cümleleri, klişe nezaket ("anlıyorum", "harika"), toksik pozitiflik, kişisel gelişim zırvaları, lafı dolandırma.
- **İstiyor:** Doğrudan, rasyonel, keskin yanıtlar. Mizah ve sarkazm serbest. Entelektüel dürüstlük şart.
- **Pattern uyarısı:** Yaratıcı tıkanma anında entelektüelleştirmeye (yeni tasarım dokümanı, rekabet analizi, platform tartışması, araç araştırması) kayma eğilimi var. Onaylanmış alışkanlık; kullanıcı bunu yüzüne söylemeni istedi. İçerik üretmeye geri çevir.
- **Geri bildirim formatı:** Hisse dair tek cümlelik nitel yargılar ("akıp gitti", "biraz zor olabilir"). Bu kelimeleri sayılara çevirip koda yansıt — kullanıcıya değil.

---

## Doğrulama (build geçti diyebilmek için)

- `psyche_mvp.html` çift tıklanınca tarayıcıda açılmalı, konsol hatası vermemeli.
- 5 dövüş arka arkaya oynanabilmeli, kart ödülü 4 kez sunulmalı, Yas'tan sonra "Koşu tamamlandı" ekranı açılmalı.
- "Yeniden" düğmesi desteyi temiz başlatmalı (eklenen ödül kartları sıfırlanmalı).

---

## Referans dokümanlar (öncelik sırasıyla)

1. **`psyche_mvp.html`** — gerçeğin tek kaynağı (kod çalışıyor demek, tasarım yaşıyor demek).
2. **Bu CLAUDE.md** — kararların güncel hâli.
3. `PSYCHE_Tasarim_Notu_v0_3.docx` — ana tasarım notu. Faz 0 kararları için bu dosyayla **çakışırsa CLAUDE.md kazanır.**
4. `psyche_kart_katalogu (1).docx` — v1.0, ~80 kart. **Faz 2+ havuzu olarak raflandı** (Kilitli Karar #3).
5. `psyche_karakterler_v01.docx`, `psyche_savas_v03.docx`, `oyunv0_2.docx`, `psyche_gdd.docx` — daha eski iterasyonlar, çelişki içerebilir.
6. `PSYCHE_Rekabet_Analizi_Raporu.docx` — pazar konumlandırması. İçeriğin büyük kısmı karar değil, gerekçe.

---

## Bakım kuralı

Bu dosyayı her **mimari** karar değişikliğinde güncelle. Sayı/denge ayarı için güncelleme. Eski sürümü silme; sayfa sonuna **DEĞİŞİKLİK KAYDI** başlığı altında tarihiyle ekle. Proje hafızasını koruyan tek dosya budur.

---

## DEĞİŞİKLİK KAYDI

### 2026-05-31 — Döngü doğrulandı; ilk his-pass + karar kartları

**Tetik:** Kullanıcı sert sürümü oynadı. Yargı: *"güzel, su gibi"* (= dişli akış, A ekseni geçti) + iki somut eksik: (1) "vuruş hissiyatı / karakter modeli yok → ham kalıyor", (2) "kartlar güzel değildi; durup okuduğum kartlar olsa süper".

**Karar kayması:** "Greybox kal, görsel/cila ekleme" kilidinin koşulu (*döngü yıpranmaya karşı dayanıklı görülene kadar*) artık karşılandı. Bu yüzden **ucuz + atılabilir** his-pass açıldı. Bespoke illüstrasyon HÂLÂ açılmadı (pahalı/yapışkan; kullanıcı "bu sanat yönü doğru" diyene kadar bekler).

**Eklenenler (`psyche_mvp.html`):**
- **His/juice:** ekran sarsıntısı (`shake`/`shake-big`), düşman flash + geri tepme, yüzen hasar sayıları (`floatNum`, crit eşiği ≥18), oyuncu hasarında kırmızı vinyet. Sıfır asset.
- **Soyut düşman formu:** arketipe göre nabız atan/morph eden CSS şekli + glif (`FORMS` tablosu). "Karakter modeli" hissinin ucuz vekili; sanat yönünü kilitlemez. Vurulunca geri teper.
- **Kart görseli:** tipe göre renkli sanat bandı + glif; "durup oku" kartlarına ⏸ işareti.
- **Karar kartları (ödül havuzuna, çekirdek deste yalın kaldı):** Yansıtma (niyet-koşullu), Boşalma (el boyutu), Dip Dalga (oynanan Savunma sayısı), Bekletilmiş Hamle (kalan Ego'yu hasara çevirir), Tortu (atık destesi boyutu). Motor: `dmgFn(S)`/`blockFn(S)`/`after(S)` + `S.player.defPlayed` sayacı.

**Açılmayan (bilinçli):** bespoke karakter/arka plan illüstrasyonu, ses/müzik, niyet-yalanı, Çözümleme ekranı, reveal/dördüncü duvar. Hâlâ Faz 1+ malzemesi.

**Sıradaki:** Kullanıcı bu sürümü oynar. (a) His yetiyor mu yoksa bespoke sanata mı geçilsin, (b) karar kartları "durup oku" hissini veriyor mu / havuz dengesi.
