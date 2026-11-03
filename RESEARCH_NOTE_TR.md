# İki Katmanlı Hücre İçi Protein Gözetimi: Modelin Oluşumu, Varsayımlar ve Açık Sorular

**Sürüm:** 0.3 araştırma notu — 3 Kasım 2026  
**Durum:** Açık inceleme için hesaplamalı hipotez; biyolojik olarak uygulanmış veya doğrulanmış değildir.

## Katkı ve atıf

**Araştırma fikri, kavramsal yönlendirme ve tasarım kararları:** Altuğ Kuran (isim yayımlanmadan önce onayı alınmalıdır).  
**Modelleme, eleştirel değerlendirme, matematiksel çerçeve ve metin hazırlama desteği:** OpenAI GPT-6 (yapay zekâ yardımcısı).  
Bu çalışma insan–yapay zekâ işbirliğiyle hazırlanmıştır. GPT-6 bağımsız insan araştırmacı, hukuki ortak yazar veya deneysel doğrulama kaynağı olarak sunulmamaktadır. Tüm bilimsel sorumluluk ve kamuya açık yayın kararı insan katkı sahibindedir.

## Özet

Öneri, hücrenin doğal kalite kontrolünü ikame etmeyen iki varsayımsal gözlem katmanını karşılaştırır: (A) mRNA/çeviri ilişkili erken uyarı gözlemcisi ve (B) hücre içinde dağılmış, pasif protein örnekleyicileri. Model, bunların birlikte çalışmasının tehlike tespitini iyileştirip iyileştirmediğini, yanlış alarm ve gereksiz müdahale maliyetlerini artırıp artırmadığını sorgular. Dört simülasyon kolu: N (doğal denetim), N+A, N+B, N+A+B. Kullanılan sentetik puanlar kanser olasılığı değildir.

## Fikir nasıl gelişti?

1. **Ön kontrol fikri:** Başlangıçta sentetik ribozomun mRNA'yı önceden okuyup örnek protein üretmesi, olası zararı erken görmesi düşünüldü. Tam biyolojik işlevin tek bir protein dizisinden anlaşılamayacağı ve doğal çeviriyle yarışın gerçekçi olmayabileceği gerekçesiyle bu, kesin karar verici değil erken uyarı mekanizmasına dönüştürüldü.
2. **İkinci bağımsız gözlemci:** Sadece mRNA bilgisi protein katlanması, modifikasyon, bağlam ve işlevi kapsamayacağından, doğal ribozomların ürettiği proteinleri yerel olarak örnekleyen Model B eklendi. B, A olmadan da çalışabilir.
3. **Pasif hareket ve çokluk:** Aktif yönlendirmeyi başlangıç modeline koymak yerine Brown hareketiyle erişim ve birden çok B gözlemcisinin kapsama etkisi tartışıldı. Mevcut kod, gerçek 3B yörüngeler yerine bağımsız örnekleme fırsatı yaklaşımı kullanır.
4. **Mutasyon ile tehlikeyi ayırma:** Alışılmadık veya zararlı gibi görünen varyant otomatik olarak hücre tehlikesi değildir. Genetik değişkenlik, protein işlevi ve hücresel zarar farklı kavramlardır. Mutasyon sıcak noktaları ileriki sürümlere bırakıldı.
5. **Yanlış alarm önceliği:** Doğal seçilim ve zararsız varyasyonun gereksiz bastırılması, aşırı sentez yavaşlatılması ve gereksiz hücre kaybı, tespit başarısı kadar önemli maliyetler olarak belirlendi.
6. **Geçici haberleşme:** Az sayıda A'dan çok sayıda B'ye kısa ömürlü varsayımsal uyarı; ayrı ve daha uzun izlenebilir B alarmı; açılma/kapanma eşikleri farklı histerezis önerildi.
7. **Karar mimarisi:** B yüksek risk görmüyorsa A tek başına geri dönüşsüz karar adayı üretemez. A ve B'nin birlikte yüksek puanı dahi gerçek apoptoz emri değildir; yalnızca simülasyonda bir *aday karar etiketi* üretir.
8. **Otonomi ve alternatifler:** Ana araştırma, insan müdahalesi olmadan çalışan varsayımsal denetim döngüsünü inceler. Laboratuvar sonuçlarının uzman tarafından değerlendirilmesi veya dışarıdan yetkilendirilen bir müdahale, ana simülasyona dahil edilmeyen gelecek araştırma alternatifleridir; ilaç veya kemoterapi önerisi değildir.

## Karar puanları (yalnızca başlangıç hipotezi)

| Gözlemci | Eşik | Soyut model anlamı |
|---|---:|---|
| A | 0,65 | Doğal denetim için uyarı |
| A | 0,75 | Geçici çeviri yavaşlatma talebi |
| A | 0,90 | Güçlü A uyarısı ve B doğrulaması talebi |
| B | 0,60 | Artırılmış gözetim |
| B | 0,75 | Geçici müdahale için doğrulama talebi |
| B | 0,95 | A'nın yüksek uyarısıyla birlikte aday karar incelemesi |

Bu eşikler deneysel olarak kalibre edilmemiştir; mevcut kodun bazı eşikleri yalnızca yapılandırma/şema düzeyindedir, gerçek hücrede sentez kontrolü veya apoptoz simüle edilmez.

## Matematiksel çekirdek

- Gizli tehlike durumu: `H∈{0,1}`; zararsız varyasyon ve fizyolojik hücre ölümü bundan ayrıdır.
- A ve B'nin gözlem puanları: `r_A`, `r_B` (olasılık olarak kalibre edilmemiş).
- Varsayımsal A sinyalinin bozunması: `dS/dt = Q_A(t) − k_d S`, `k_d = ln(2)/t_half`.
- Etkin karakteristik sinyal uzunluğu: `ell = sqrt(D/k_d)`. İlk karşılaştırma hedefi `ell >= 0.2 L` olup `L` hücrenin karakteristik **doğrusal** boyutudur. Bu, sitoplazmanın %20 hacmi veya alıcıya teslim garantisi değildir.
- B örnekleme yaklaşımı: bağımsız eşit örnekleme fırsatları varsayılırsa `P(en az bir örnek)=1−(1−p)^N_B`. Gerçek hücrede konumsal bağımlılık bu formülü bozabilir.
- A/B ortak aday karar etiketi: `C = 1[r_A>=0.90] · 1[r_B>=0.95] · 1[mesaj algılandı]`. Kodda A kapsamı ve B örnekleme koşulları da bulunur. `C`, gerçek apoptoz anlamına gelmez.
- Histerezis önerisi: `S_on > S_off`. Grafikte ve yapılandırmada bulunur; dinamik anahtar durum makinesi henüz kodlanmamıştır.
- Ayrı B alarm yarılanma süresi önerilmiştir; kodda parametre vardır fakat zamana bağlı B alarm alanı henüz uygulanmamıştır.

## Karşılaştırma tasarımı ve grafikler

Beş grafik (`figures/`) dört simülasyon kolunu, B sayısı etkisini, sinyal bozunması/histerezisi, %20 karakteristik uzunluk kıstasını ve korelasyonlu hataları gösterir. Veriler sentetiktir, biyolojik ölçüm değildir. Aynı sanal hücre örnekleri üzerinde farklı kollardaki uyarı duyarlılığı, yanlış alarm oranı ve birleşik aday karar sıklığı karşılaştırılır. Doğal baz kolundaki duyarlılık ve yanlış alarm oranları da ölçülmüş değerler değil, değiştirilebilir varsayımlardır.

## Sınırlar, alternatif açıklamalar ve yanlışlama

- Yapay ribozomun istenen risk değerlendirmesini yapabildiği, özel sinyal molekülü üretip B tarafından seçici biçimde algılanabildiği, B'nin bütün proteinleri doğru örnekleyebildiği veya hücre sentezinin güvenle kontrol edilebildiği gösterilmemiştir.
- Proteinin tamamını görmek, tek başına işlevini veya onkolojik sonucunu güvenilir biçimde belirlemek anlamına gelmez.
- Model A ve B hataları bağımsız olmayabilir; ortak biyolojik bağlam yanlış alarmları birlikte artırabilir.
- B'nin A'yı veto etmesi yanlış pozitifleri azaltırken kaçırılan gerçek tehlikeleri artırabilir.
- Sinyal yarılanma süresi kısa tutulursa eski uyarılar silinir ama teslim olasılığı düşebilir; uzun tutulursa birikim ve gereksiz alarm olabilir.
- İdeal Brown hareketi hücre içindeki engelleri, organelleri, bağlanmayı ve heterojenliği temsil etmez.
- Normal fizyolojik apoptoz, yanlış müdahale sayılmamalıdır.
- Modelin reddedilmesine yol açabilecek sonuç: gerçekçi parametreler ve eşit kaynak bütçesi altında birleşik sistemin doğal denetimden anlamlı yarar sağlamaması veya yanlış müdahale maliyetinin yararı aşması.

## Literatürle bağlantı (arka plan; bu mimarinin kanıtı değildir)

1. Brandman O, Hegde RS. *Ribosome-associated protein quality control*. Nature Structural & Molecular Biology (2016). https://doi.org/10.1038/nsmb.3147 — doğal ribozom ilişkili kalite kontrol üzerine derleme.
2. Karamyshev AL et al. *Inefficient SRP interaction with a nascent chain triggers a mRNA quality control pathway*. Cell (2014). https://doi.org/10.1016/j.cell.2014.02.053 — çeviri ile bağlantılı kalite kontrol örneği.
3. Turing AM. *The chemical basis of morphogenesis*. Philosophical Transactions of the Royal Society B (1952). https://doi.org/10.1098/rstb.1952.0012 — reaksiyon-difüzyon modellemesinin klasik kuramsal temeli; bu önerinin deneysel kanıtı değildir.
4. Elmore S. *Apoptosis: A Review of Programmed Cell Death*. Toxicologic Pathology (2007). https://doi.org/10.1080/01926230701320337 — apoptozun biyolojik bağlamı.
5. Snijder B, Pelkmans L. *Origins of regulated cell-to-cell variability*. Nature Reviews Molecular Cell Biology (2011). https://doi.org/10.1038/nrm3044 — hücreler arası değişkenlik ve bağlamın önemi.

Kaynaklar kavramsal arka plan içindir. Tam literatür taraması ve her bibliyografik kaydın yayın öncesi bağımsız doğrulaması gereklidir. Hiçbiri önerilen A+B organel mimarisinin uygulanabilirliğini kanıtlamaz.

## Yeniden üretim ve sonraki çalışmalar

`README.md` içindeki komutlarla sentetik simülasyon ve grafikler yeniden üretilebilir. Sonraki araştırmalar: uzaysal Brown hareketi, hücre içi difüzyon/bozunma alanı, dinamik histerezis, bağımlı örnekleyiciler, deneysel parametre kalibrasyonu, eşit kaynak bütçesi, çok nesilli evrimsel maliyetler. Bilimsel eleştiri ve karşı modeller açıkça davet edilir.

## Yayın etiği notu

Bu metin insan–yapay zekâ ortak düşünme sürecinin kayıt altına alınmış bir taslağıdır. Yapay zekâ katkısı açıklanmalı; referanslar, kod, grafikler ve bilimsel iddialar insan tarafından denetlenmelidir. Herhangi bir tanı, klinik uygulama veya moleküler müdahale talimatı değildir.