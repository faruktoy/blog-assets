---
title: "FDM Baskılarda Yüzey Kalitesini Artırmak: PLA vs ABS vs PETG"
date: "30 Nisan 2026"
readTime: "12 dk okuma"
tags: "3D Baskı, FDM, Yüzey Pürüzlülüğü, Ra, Araştırma"
---

# FDM Baskılarda Yüzey Kalitesini Artırmak: PLA vs ABS vs PETG

> Bir 3D baskı ne kadar iyi görünür? Bu sorunun teknik cevabı yüzey pürüzlülüğü — Ra değeri — ile ölçülür. Bu yazıda kendi baskı deneyimlerimi, Araştırma Yöntemleri dersinde incelediğim makaleyi ve uluslararası literatürden dört farklı çalışmayı çapraz karşılaştırarak, FDM'de yüzey kalitesini gerçekten neyin belirlediğini anlatıyorum.

## Ra Nedir ve Neden Önemli?

Yüzey pürüzlülüğü (Ra), bir yüzeydeki mikro düzensizliklerin aritmetik ortalamasıdır. FDM baskılarda bu değer genellikle 1–15 µm arasında değişir. Düşük Ra = pürüzsüz yüzey demek.

Neden önemli? Ben gerçek uçak parçalarından ölçü alarak hediyelik plaket ve sergileme modelleri basıyorum — bir Pitot tüpünün, AOA sensörünün veya Ice Detector'ın birebir maketi. Bu tür parçalarda yüzey kalitesi doğrudan görsel başarıyı belirliyor: pürüzlü bir model hediye edemezsiniz. Fonksiyonel parçalarda ise Ra, montaj uyumu ve estetik açıdan kritiktir.

Literatürde bu konuda önemli bir boşluk var: çoğu çalışma tek malzeme üzerinden parametre optimizasyonu yaparken, farklı filamentleri aynı koşullarda karşılaştıran çalışmalar görece sınırlı. Bu yazıda birden fazla kaynağı bir araya getirerek daha bütüncül bir tablo çizmeye çalışıyorum.

## Filament Karşılaştırması: PLA, ABS, PETG

Geçen dönem Araştırma Yöntemleri dersinde incelediğim Kovan vd. makalesi, bu üç filamenti Taguchi L27 deney planıyla aynı koşullarda karşılaştırıyor. Sonuçlar:

- PLA, Ra açısından ABS'den %7,23, PETG'den %54,19 daha iyi yüzey vermiş.
- Çekme dayanımında da PLA sırasıyla %46 ve %34 önde.

Bu bulgular tek başına değil. Portoacă vd. (2023, Polymers) ABS ve PLA üzerinde yaptıkları çalışmada, dolgu oranı artırılıp ekstrüzyon sıcaklığı 220°C'ye ayarlandığında kırılma yükünün arttığını göstermiş. İlginç olan şu: Kovan'ın çalışmasında PLA'nın Ra avantajı net iken, Portoacă'nın sonuçları ABS'nin doğru sıcaklık ve dolgu ile yüzey-dayanım dengesinde rekabetçi olabileceğini gösteriyor.

PETG tarafında ise Mishra vd. (2023, Polymers) yalnızca PETG'ye odaklanarak RSM ve ANFIS modelleriyle optimum parametreleri belirlemiş: 50 mm/s hız, 0,1 mm katman, 230°C sıcaklık ve 0,6 mm raster genişliği. Kovan'ın çalışmasında PETG en kötü Ra'yı verirken, Mishra'nın PETG-spesifik optimizasyonu çok daha iyi sonuçlar elde etmiş — bu da "kötü malzeme" diye bir şey olmadığını, parametrelerin malzemeye özel ayarlanması gerektiğini kanıtlıyor.

Kendi deneyimlerimde genellikle ABS tercih ediyorum. Evet, Ra açısından PLA daha iyi yüzey verebiliyor ama ABS'nin UV dayanımı, ısı direnci ve darbe tokluğu sergileme modelleri için çok daha uygun — güneş alan bir rafta PLA erir, ABS dayanır. ABS'de katmanlar arası çizgiler biraz daha belirgin, PETG ise "ıslak" bir görünüm bırakıyor.

ABS'nin en büyük dezavantajı VOC (uçucu organik bileşik) emisyonu. Baskı sırasında stiren gazı salınımı olur; kapalı hazne ve iyi havalandırma şart. Küçük bir odada havalandırmasız ABS basmak sağlık açısından riskli — ben baskılarımı havalandırmalı ortamda yapıyorum.

Sonuç olarak "en iyi filament" diye bir şey yok — hedefe göre değişir. Sergileme ve dayanıklılık istiyorsanız ABS, en pürüzsüz yüzey istiyorsanız PLA, kimyasal direnç ve esneklik istiyorsanız PETG.

## Katman Yüksekliği: En Belirleyici Parametre

Bu konuda literatürde geniş bir konsensüs var. Kovan vd. çalışmasında katman yüksekliği en baskın faktör olarak çıkarken, Pérez vd. (2018, Materials) bunu bağımsız olarak doğrulamış. Pérez'in PLA üzerinde yaptığı ANOVA analizinde, yalnızca katman yüksekliği ve duvar kalınlığının yüzey pürüzlülüğü üzerinde istatistiksel olarak anlamlı etkisi olduğu görülmüş — baskı hızı ve sıcaklık anlamlı çıkmamış.

Daha da çarpıcısı, 2025'te yayımlanan bir Springer çalışmasında (Int J Adv Manuf Technol), katman yüksekliğinin yüzey pürüzlülüğü varyansının %66'sına kadar açıklayabildiği raporlanmış. Bu oran inanılmaz yüksek — tek bir parametre, sonucun üçte ikisini belirliyor.

Somut rakamlarla (Kovan vd.):

- 0,1 mm katman → Ra ~1,44 µm (en iyi yüzey)
- 0,2 mm katman → Ra ~4–6 µm (standart)
- 0,3 mm katman → Ra ~8–12 µm (kaba ama hızlı)

Bunun fiziksel nedeni "merdiven etkisi" (staircase effect): kalın katmanlar eğimli ve kavisli yüzeylerde basamak gibi belirgin izler bırakır. Pérez'in çalışması bunu açıkça vurgularken, Kovan'ın SEM görüntüleri kırılma yüzeylerinde bu etkinin kanıtını sunuyor.

Kendi P3Steel yazıcımda 0,1 mm ile bastığım parçalar neredeyse enjeksiyonla üretilmiş gibi görünüyor. Ama bir sorun var: baskı süresi 3 kata çıkıyor. Bu yüzden prototiplerde 0,2 mm, sadece final parçalarda 0,1 mm kullanıyorum.

## Hız ve Sıcaklık: Kaynaklar Ne Diyor?

Baskı hızının etkisi konusunda kaynaklar ilginç bir şekilde ayrışıyor — ve bu aslında değerli bir bilgi.

Kovan vd. çalışmasında en iyi Ra değeri 60 mm/s'de elde edilmiş; 40 mm/s değil. Bu "yavaş = iyi" varsayımını çürütüyor. Mishra vd. ise PETG için optimum hızı 50 mm/s olarak bulmuş. Pérez vd. ise hızın Ra üzerinde istatistiksel olarak anlamlı bir etkisi olmadığını söylüyor.

Bu çelişki gibi görünen durum aslında şunu anlatıyor: hızın etkisi malzemeye, yazıcı mekaniğine ve diğer parametrelerin seviyelerine bağlı olarak değişiyor. Kovan'ın Taguchi tasarımında hız etkisi dolgu oranı ve tarama açısıyla birlikte ortaya çıkıyor; Pérez'de ise izole edildiğinde anlamsız kalıyor. Benim deneyimimde 50–65 mm/s arası "tatlı nokta" oluyor.

Sıcaklık konusunda daha net bir tablo var:

- PLA: 200–210°C arası en temiz yüzey (Portoacă vd. 220°C'yi mekanik dayanım için önerirken, yüzey için biraz düşük tutmak gerekiyor)
- ABS: 230–240°C, ama kapalı hazne şart — Portoacă'nın çalışması bunu doğruluyor
- PETG: 230°C (Mishra vd. optimumu), fazla sıcak olursa stringing başlıyor

Sıcaklık kulesi (temperature tower) basarak kendi filamentinizin ideal sıcaklığını bulmak en güvenilir yöntem.

## Z Wobble: Sessiz Yüzey Katili

Parametre optimizasyonu yaptınız, filamenti doğru seçtiniz ama baskıda düzensiz çizgiler mi var? Muhtemelen Z wobble sorunuyla karşı karşıyasınız. Literatür genellikle yazılımsal parametrelere odaklanır ama mekanik hatalar tüm optimizasyonu geçersiz kılabilir.

Z wobble, Z eksenindeki vida (leadscrew) ile motor arasındaki hizalama bozukluğundan kaynaklanan periyodik bir yüzey hatasıdır. Belirtileri:

- Yüzeyde düzenli aralıklarla tekrarlanan dalgalanma
- Katman yüksekliğinden bağımsız, baskı yüksekliğine yayılan çizgiler
- Parçayı döndürdüğünüzde her tarafta aynı desende görülmesi

Bu sorun akademik çalışmalarda "staircase effect"ten farklı olarak ele alınır: staircase etkisi katman yüksekliğiyle doğrusal, Z wobble ise mekanik hizalamayla ilgilidir. Pérez'in çalışmasında hız ve sıcaklığın Ra'yı anlamlı etkilememesinin bir nedeni de test yazıcısının mekanik olarak iyi kalibre edilmiş olması olabilir — bu değişkenler ancak mekanik sorunlar çözüldükten sonra anlam kazanıyor.

P3Steel yazıcımı kurarken bu sorunla çok uğraştım. Çözüm adımlarım:

1. Leadscrew coupler'ı esnek (jaw coupler) olanla değiştirdim — rijit bağlantı hizalama hatasını doğrudan yüzeye taşıyor.
2. Z motorunu leadscrew ile aynı eksene hizaladım (bir cetvelle bile kontrol edebilirsiniz).
3. Anti-backlash nut ekledim — hem wobble hem de Z banding azaldı.

Bu üç adımdan sonra Ra değerimde gözle görülür iyileşme oldu.

## Kalite mi, Dayanım mı? Çapraz Karşılaştırma

Kovan vd. makalesinin en önemli bulgusu: en iyi yüzey kalitesi ve en iyi çekme dayanımı için optimum parametreler farklı.

- En düşük Ra: PLA – %60 dolgu – 0,1 mm katman – 60 mm/s – 30° tarama açısı → Ra 1,44 µm
- En yüksek dayanım: PLA – %60 dolgu – 0,3 mm katman – 40 mm/s – 45° tarama açısı → 32,18 MPa

Katman yüksekliği ve hız tam ters yönde. İnce katman pürüzsüz yüzey veriyor ama katmanlar arası yapışma azalıyor. 2023 SFF Symposium'da sunulan bir çalışmada, katman yüksekliğini 0,1'den 0,2 mm'ye ikiye katlamanın çekme dayanımını %6–11 düşürdüğü gösterilmiş.

Portoacă vd. bu dengeye farklı bir açıdan yaklaşıyor: dolgu oranı artırarak ve sıcaklığı optimize ederek hem yüzey hem dayanım iyileştirilebilir. Mishra vd. ise PETG'de çok amaçlı optimizasyon (NSGA-II) kullanarak Pareto frontu oluşturmuş — yani kalite-dayanım dengesinde birden fazla "doğru cevap" olduğunu matematiksel olarak göstermiş.

Bu yüzden "bu parça ne iş yapacak?" sorusu her baskıdan önce sorulmalı. Uçak parçası modellerimde dış yüzeyi 0,1 mm ile basıp iç dolguyu %60'da tutuyorum — yüzey kalitesi ile dayanım arasında bir uzlaşma.

## Sonuç: Kendi Parametreni Bul

Beş farklı akademik çalışmayı karşılaştırdığımızda ortaya çıkan tablo net: katman yüksekliği her yerde baskın faktör, ama diğer parametrelerin etkisi malzemeye ve yazıcı mekaniğine göre değişiyor. Tek bir reçete yok.

Benim önerilerim:

1. Sıcaklık kulesi ile başlayın — filamentinizin gerçek davranışını görün.
2. Katman yüksekliğini parçanın amacına göre seçin, otomatik pilota almayın.
3. Z ekseninizi kontrol edin — mekanik sorunlar yazılımla çözülemez.
4. Tek seferde tek parametre değiştirin; yoksa neyin ne etkilediğini anlayamazsınız.
5. Malzemeye özel optimizasyon yapın — Kovan'ın genel karşılaştırması yol gösterici, ama Mishra'nın PETG çalışmasının gösterdiği gibi malzeme-spesifik ayar çok daha iyi sonuç veriyor.

## Kaynaklar

[1]: https://dergipark.org.tr/en/download/article-file/3434449 "Kovan vd., FDM Yöntemiyle Üretilen ABS, PLA ve PETG Numunelerin Yüzey Pürüzlülüğü ve Çekme Dayanımının Modellenmesi ve Optimizasyonu"
[2]: https://doi.org/10.3390/ma11081382 "Pérez, M. et al. (2018), Surface Quality Enhancement of FDM Printed Samples Based on the Selection of Critical Printing Parameters, Materials, 11(8), 1382"
[3]: https://doi.org/10.3390/polym15163419 "Portoacă, A.I. et al. (2023), Optimization of 3D Printing Parameters for Enhanced Surface Quality and Wear Resistance, Polymers, 15(16), 3419"
[4]: https://doi.org/10.3390/polym15030546 "Mishra, P. et al. (2023), Parametric Modeling and Optimization of Dimensional Error and Surface Roughness of FDM Printed PETG Parts, Polymers, 15(3), 546"
[5]: https://doi.org/10.1007/s00170-025-14820-2 "Evaluating the Influence of Machine Type on Surface Roughness in Material Extrusion (2025), Int J Adv Manuf Technol"
