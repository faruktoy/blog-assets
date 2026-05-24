---
title: "C-130, T56, R391 ve Değişken Hatveli Pervane Mantığı"
date: "21 Mayıs 2026"
readTime: "~20 dk okuma"
tags: "N/A"
---

# C-130, T56, R391 ve Değişken Hatveli Pervane Mantığı
> T56 motoru ve sabit hız pervane sistemini canlandıran 3D baskılı eğitim modeli. Kontrol mantığı, NTS, feather ve air start döngüleri.

## 3D Turboprop Demonstratör Modeli Üzerinden Teknik Bir İnceleme

Turboprop motorlarda asıl mesele yalnızca motorun dönmesi değildir. Motor gücünün pervaneye nasıl aktarıldığı, pervane RPM'inin nasıl kontrol edildiği, pal açısının nasıl değiştiği ve governor sisteminin bu değişkenleri nasıl dengelediği birlikte düşünülmelidir. Özellikle C-130 gibi büyük turboprop uçaklarda pervane, yalnızca dönen bir itki elemanı değil; motor gücünü havaya aktaran aktif bir kontrol sistemidir.

Bu yazıda C-130 ailesindeki T56 motoru, 54H60 pervane sistemi, R391 pervane geometrisi, constant-speed propeller mantığı ve bunların 3D bir turboprop demonstratör modelinde nasıl temsil edilebileceği teknik olarak ele alınmaktadır.

Bu projede kullanılan temel 3D geometri Cadly turboprop modelinden alınmıştır. Ancak modelde yazılım ve elektronik tarafı basit bir "prop-power lever" gösterimi olarak bırakılmamış; Condition Lever, Power Lever, AIR START animasyonu, toggle switch ile seçilebilen iki farklı RUN mantığı, servo kontrollü pal açısı hareketi ve DC motorla temsil edilen pervane dönüşüyle daha öğretici bir demonstratöre dönüştürülmüştür.

<!-- GÖRSEL TUTUCU: Fotoğraf
     Açıklama: 3D baskı turboprop demonstratör modelinin genel görünümü
     SearchKeywords: 3D printed turboprop propeller pitch demonstrator model -->

---

## C-130 Ailesinde Motor ve Pervane Mantığı

C-130 ailesi uzun yıllardır farklı motor ve pervane kombinasyonlarıyla kullanılmıştır. Klasik C-130E/H gibi modellerde Allison, güncel adıyla Rolls-Royce T56 turboprop motoru kullanılır. Rolls-Royce, T56'yı "single shaft, modular design" bir turboprop motor olarak tanımlar. Aynı kaynakta T56'nın 14 kademeli aksiyel kompresör, 4 kademeli türbin ve iki kademeli redüksiyon dişli kutusu içerdiği; redüksiyon dişli kutusunda propeller brake bulunduğu ve sistemin torquemeter assembly üzerinden power section ile ilişkilendirildiği belirtilir. ([Rolls-Royce][1])

C-130J Super Hercules tarafında ise Rolls-Royce AE2100D3 motoru ve Dowty/GE Aerospace R391 altı pal kompozit pervane sistemi kullanılır. AE2100D3'ün C-130J ve LM-100J transport uçaklarında kullanıldığı Rolls-Royce tarafından belirtilir. ([Rolls-Royce][2]) R391 ise hydraulic constant-speed, counterweight, reversible ve full-feathering özellikli modern bir pervanedir. Smithsonian kaynağı R391'in altı kompozit pal yapısına ve yaklaşık 4,115 m çapa sahip olduğunu belirtir. ([National Air and Space Museum][3])

Bu projede 3D modelin R391 görünümünden esinlenmesi, modelin doğrudan gerçek bir C-130J kokpit kontrol kopyası olduğu anlamına gelmez. R391 görsel olarak daha modern ve dikkat çekici durduğu için tercih edilmiştir. Kontrol mantığı ise C-130 ailesindeki özellikle T56/54H60 sisteminde görülen Power Lever, Condition Lever, governor, feather, ground stop ve air-start kavramlarını anlatabilecek şekilde yazılım üzerinden kurgulanmıştır.

<!-- TABLO: C-130 Ailesi Motor ve Pervane Karşılaştırması -->

| Özellik | C-130E/H | C-130J Super Hercules |
|---|---|---|
| Motor | Allison/Rolls-Royce T56-A-15 | Rolls-Royce AE2100D3 |
| Motor tipi | Single-shaft turboprop | Free-turbine turboprop |
| Pervane | Hamilton Sundstrand 54H60 | Dowty/GE Aerospace R391 |
| Pal sayısı | 4 | 6 |
| Pervane çapı | ~4,11 m (13 ft 6 in) | ~4,115 m (13 ft 6 in) |
| Pervane malzemesi | Alüminyum alaşım | Kompozit |
| Pervane özellikleri | Hydraulic constant-speed, feathering, reversing | Hydraulic constant-speed, counterweight, full-feathering, reversing |
| Motor kontrol | Hydromechanical fuel control + TD system | FADEC (Full Authority Digital Engine Control) |
| Pervane RPM (takeoff) | ~1021 RPM | ~1020,7 RPM |

<!-- GÖRSEL TUTUCU: Fotoğraf
     Açıklama: Allison/Rolls-Royce T56 motor ve 54H60 pervane sistemi
     SearchKeywords: Allison T56 engine 54H60 propeller C-130H -->

<!-- GÖRSEL TUTUCU: Fotoğraf
     Açıklama: Dowty R391 altı pal C-130J pervane görünümü
     SearchKeywords: Dowty R391 six blade propeller C-130J -->

---

## Constant-Speed Propeller Mantığı

Turboprop sistemlerde en kritik kavramlardan biri constant-speed propeller mantığıdır. Constant-speed sistemde amaç, pervane RPM'ini belirli bir hedef değere yakın tutmaktır. Motor daha fazla güç üretmek istediğinde pervane hızlanma eğilimi gösterir. Governor sistemi bunu algılar ve pal açısını değiştirerek pervanenin daha fazla aerodinamik yük almasını sağlar. Böylece motor gücü artarken pervane RPM'i sabite yakın tutulur.

C-130 uçuş manuelinde pervane hızının Flight Range içinde propeller governing system tarafından constant RPM tutulacak şekilde kontrol edildiği, Ground Range içinde ise pal açısının throttle lever konumuna bağlı olduğu belirtilir. Aynı bölümde low pitch stop'un Flight Range içinde pal açısının yaklaşık 23° altına düşmesini engellediği açıklanır. ([Uniforce-SOG][4])

T56 tarafında 100% motor devri yaklaşık 13.820 RPM'dir. Lockheed Martin Service News kaynağı, 13.54:1 redüksiyon oranı ile bunun pervane tarafında yaklaşık 1021 RPM'ye karşılık geldiğini belirtir. ([Lockheed Martin][5]) R391 tarafında da benzer constant-speed karakter vardır; R391 tip sertifika verisinde takeoff propeller speed değeri 1020,7 RPM, maximum continuous propeller speed değeri ise 1020,7 RPM olarak verilir. ([CAA][6])

Buradaki önemli sonuç şudur: C-130 ailesindeki gerçek constant-speed mantığında Power Lever ileri alındığında pervane RPM'i sürekli artmaz. Normal uçuşta RPM sabite yakın tutulur; değişen şey daha çok tork, yakıt akışı ve pal açısıdır.

<!-- DİYAGRAM TUTUCU: Governor Çalışma Prensibi
     Açıklama: Constant-speed propeller governor'ın pilot valve, flyweight ve blade angle feedback döngüsünü gösteren şematik diyagram
     SearchKeywords: constant speed propeller governor pilot valve flyweight schematic -->

<!-- GRAFİK TUTUCU: RPM vs Power Lever Pozisyonu
     Açıklama: Constant-speed sistemde Power Lever ileri alındıkça RPM'in sabite yakın kaldığını, pal açısı ve torkun arttığını gösteren çizgi grafik
     Eksenler: X = Power Lever pozisyonu (%) | Y₁ = Pervane RPM | Y₂ = Pal açısı (°) | Y₃ = Tork (ft-lbs)
     SearchKeywords: constant speed propeller RPM torque blade angle vs power lever graph -->

---

## Pal Pitch, Pal Açısı ve Feather Kavramı

Bu yazıda "pervane" kelimesi tüm propeller assembly için, "pal" kelimesi ise pervanenin tekil kanat elemanları için kullanılacaktır.

Pal pitch veya pal açısı, her bir palin hava akışına göre aldığı açıyı ifade eder. Düşük pal açısında pal havayı daha az "ısırır" ve pervane daha kolay döner. Yüksek pal açısında ise pal her dönüşte daha fazla hava ile etkileşime girer ve pervane daha fazla aerodinamik yük oluşturur.

Genel constant-speed propeller eğitiminde low pitch / high RPM kombinasyonu kalkış için, higher pitch / lower RPM kombinasyonu ise seyir için kullanılabilir. FAA eğitim materyalinde de low-pitch/high-RPM ayarının takeoff için, daha yüksek pitch ve daha düşük RPM ayarının uçuş sonrası kullanılabileceği açıklanır. ([Federal Aviation Administration][7]) Ancak C-130/T56 gibi sistemlerde bu ilişki doğrudan Power Lever üzerinden birebir okunmaz; çünkü uçuş aralığında pervane RPM'i governor tarafından sabite yakın tutulur. ([Uniforce-SOG][4])

Feather ise pallerin hava akışına daha paralel hâle getirildiği bayraklama konumudur. Motor arızası veya motor durdurma durumunda feather, pervane sürüklemesini azaltmak için kullanılır. R391 pervane sistemi de full-feathering özelliklidir. ([National Air and Space Museum][3])

<!-- TABLO: Modelde Kullanılan Temsilî Pal Açısı Değerleri -->

| Çalışma Bölgesi | Temsilî Pal Açısı | Açıklama |
|---|---|---|
| Low Pitch / Ground | ~0° – 5° | Pervane minimum aerodinamik yükte |
| Flight Idle / Low Pitch Stop | ~23° | Governor tarafından izin verilen minimum uçuş açısı |
| Takeoff / Climb | ~23° – 35° | Yüksek güç, artan pal açısı |
| Cruise / High Pitch | ~35° – 55° | Seyir verimi için yüksek pal açısı |
| Full Feather | ~93° | Pal hava akışına paralel; minimum sürükleme |

> **Not:** Bu değerler uçuşa elverişli bir kontrol datası değildir. Modelin amacı, pal açısı davranışını görsel ve eğitsel olarak anlaşılır hâle getirmektir.

<!-- DİYAGRAM TUTUCU: Pal Açısı Karşılaştırması
     Açıklama: Aynı pervane palinın low pitch, cruise pitch ve feather konumlarındaki açısal durumunu gösteren yan yana üç kesit görünümü
     SearchKeywords: propeller blade angle low pitch high pitch feather cross section comparison diagram -->

---

## Reverse Neden Şimdilik Yok?

Gerçek turboprop sistemlerde reverse thrust, pal açısının sıfırın altına geçmesiyle veya negatif pitch bölgesine alınmasıyla oluşturulur. R391 tip sertifika verisinde pervanenin variable-pitch, constant-speeding, feathering ve reversing tipte olduğu; beta control ile aircraft braking ve ground manoeuvring için manuel pitch selection sağlandığı belirtilir. ([CAA][6])

Ancak bu 3D demonstratör modelinde mekanik tasarım şu an negatif pal açısı bölgesini desteklememektedir. Bu yüzden reverse modu yazılım mantığında bilinse de fiziksel modelde uygulanmamıştır. Modelin mevcut versiyonu düşük pozitif pal açısı, flight idle, climb/cruise temsili, feather ve air-start/unfeather hareketlerine odaklanmaktadır.

Bu durum modelin sınırlaması olarak kabul edilmiştir. İleride mekanik bağlantı ve servo hareket aralığı negatif pal açısını destekleyecek şekilde revize edilirse reverse bölgesi de ayrı bir gösterim modu olarak eklenebilir.

<!-- DİYAGRAM TUTUCU: Reverse Pitch Mantığı
     Açıklama: Pozitif pitch, sıfır pitch ve negatif (reverse) pitch konumlarında pal ve hava akışı yönü ilişkisini gösteren diyagram
     SearchKeywords: propeller reverse pitch negative blade angle airflow direction diagram -->

---

## 3D Demonstratör Modelinin Amacı

Bu 3D demonstratör, gerçek bir C-130 pervane sisteminin birebir çalışan kopyası değildir. Gerçek uçakta hydraulic governor, propeller control unit, fuel control, torquemeter, redüksiyon dişli kutusu, NTS sistemi, aerodinamik yükler ve uçuş şartları birlikte çalışır.

Modelde ise bu karmaşık sistem; servo motor, DC motor, potansiyometre lever'lar, amber LED, toggle switch ve yazılım eğrileri ile temsil edilmektedir.

Modelin üç ana görsel hedefi vardır:

1. **Pal açısı değişimini göstermek** — Servo motorla kontrol edilen pal açısının Power Lever hareketine nasıl bağlandığını fiziksel olarak sergilemek.
2. **Pervane dönüş hızı temsilini göstermek** — DC motor PWM değerinin farklı çalışma modlarında nasıl değiştiğini veya sabit kaldığını göstermek.
3. **AIR START / unfeather sürecini görselleştirmek** — Amber LED ve lineer pal açısı animasyonu ile feather'dan çıkış sürecini adım adım göstermek.

Bu nedenle model bir uçuş simülatörü değil; teknik eğitim ve sunum için hazırlanmış bir turboprop pervane kontrol demonstratörüdür.

<!-- GÖRSEL TUTUCU: Fotoğraf
     Açıklama: Servo kontrollü pal açısı mekanizmasının yakın çekim fotoğrafı
     SearchKeywords: servo controlled variable pitch propeller mechanism model closeup -->

---

## Power Lever ve Condition Lever Ayrımı

C-130 ailesinde motor kontrol mantığını anlamak için Power Lever ve Condition Lever ayrımı önemlidir. C-130 uçuş manuelinde dört adet pedestal-mounted condition lever'ın engine starting/stopping ve propeller feathering/unfeathering için primary controls olduğu belirtilir. Bu lever'lar hem mekanik bağlantıları hem de elektriksel kontrol sağlayan switch'leri çalıştırır. Manuelde Condition Lever için dört placarded position tanımlanır: RUN, AIR START, GROUND STOP ve FEATHER. ([Uniforce-SOG][4])

**Power Lever**, pilotun güç talebini belirleyen ana koldur. Flight Range içinde motor gücü ve governor sistemi birlikte çalışır; Power Lever ileri alındığında sistem daha fazla güç/tork talebini temsil eder ve governor pal açısını değiştirerek pervane RPM'ini sabite yakın tutmaya çalışır. Ground Range içinde ise pal açısı doğrudan throttle lever konumunun fonksiyonu hâline gelir ve pervane RPM governing mantığı uçuş aralığındaki gibi çalışmaz. ([Uniforce-SOG][4])

**Condition Lever** ise doğrudan "pal açısı kolu" gibi düşünülmemelidir. C-130/T56 mantığında bu kol motorun çalışma durumunu, yakıt/ignition kontrolünü, feather/unfeather sinyallerini ve air-start sürecini yönetir.

<!-- TABLO: Condition Lever Pozisyonları ve İşlevleri -->

| Pozisyon | Tip | İşlev |
|---|---|---|
| **RUN** | Detent (kilitli) | Engine fuel ve ignition sistemlerini speed-sensitive control altına alır. Bu konumda Condition Lever'ın pervane üzerinde doğrudan kontrolü yoktur. |
| **AIR START** | Yay kuvvetine karşı tutulur | RUN ile aynı switch'i kapatır; ek olarak propeller auxiliary pump'ı çalıştırarak pervaneyi unfeather etmek için hidrolik basınç sağlar. |
| **GROUND STOP** | Detent (kilitli) | Touchdown sistemi yer modundaysa elektrikli yakıt kapatma valfini kapatır. Nacelle preheat devre kontrolünü de sağlar. |
| **FEATHER** | Mekanik bağlantı + switch | Engine-mounted coordinator üzerinden pervaneye ve fuel control shutoff valve'a mekanik hareket iletir; pervaneye mekanik ve elektriksel feather sinyali verir. |

*Kaynak: C-130 Flight Manual, CGTO 1C-130-1 ([Uniforce-SOG][4])*

Modelde Condition Lever için kullanılan demonstratör modları:

| Gerçek Pozisyon | Model Modu | Demonstratör Davranışı |
|---|---|---|
| FEATHER | PROP FEATHER | Motor PWM = 0, pal açısı → 93°, Power Lever yok sayılır |
| GROUND STOP | PROP DEMO | Motor çalışmaz, Power Lever ile yalnızca pal açısı değişir |
| RUN | NORMAL OPERATION | Toggle switch'e göre iki farklı PWM–pal açısı eğrisi |
| AIR START | UNFEATHER DEMO | LED animasyonu + lineer pal açısı geçişi (93° → 23°) |

<!-- GÖRSEL TUTUCU: Fotoğraf
     Açıklama: C-130 kokpitinde power lever ve condition lever'ların pedestal üzerindeki yerleşimi
     SearchKeywords: C-130 cockpit throttle quadrant power lever condition lever pedestal -->

---

## GROUND STOP ve GROUND IDLE Terminoloji Ayrımı

Bu noktada terminoloji özellikle önemlidir. Gerçek C-130E/H/T56 mantığında **GROUND STOP**, Condition Lever üzerindeki bir konumdur ve motoru durdurmak için kullanılır. Buna karşılık **GROUND IDLE**, Power Lever / throttle tarafındaki yer çalışma konumuyla ilişkilidir; Flight Idle'ın altındaki beta aralığında, pervane kanatlarının düşük pozitif pitch'te olduğu ve motorun minimum yer devrinde çalıştığı konumdur.

Uçuş manuelinde engine shutdown sırasında "throttles in ground idle" kontrol edilirken condition lever'ların GROUND STOP konumuna alınması istenir. Yani Ground Idle ve Ground Stop aynı kontrol kolunun aynı konumu değildir; farklı kollardaki farklı konumlardır. ([Uniforce-SOG][4])

<!-- TABLO: GROUND STOP vs GROUND IDLE Karşılaştırması -->

| Terim | Hangi Kol | İşlev | Konum |
|---|---|---|---|
| **GROUND STOP** | Condition Lever | Motor durdurma (yakıt kesme) | Detent pozisyon |
| **GROUND IDLE** | Power Lever (Throttle) | Minimum yer çalışma gücü | Flight Idle altındaki detent |

Bu yüzden modelde **GROUND STOP / PROP DEMO** ifadesi kullanılmaktadır. Buradaki GROUND STOP, Condition Lever tarafındaki gerçek C-130 konumuna karşılık gelir. PROP DEMO ise modelin eğitim amaçlı ek davranışıdır; gerçek uçakta bu şekilde bir gösterim modu yoktur.

---

## FEATHER / PROP FEATHER Modu

FEATHER modunda model, motor arızası veya motor kapatma sonrası pervanenin bayraklama konumuna alınmasını temsil eder.

Bu modda motor PWM değeri sıfıra çekilir, pal açısı yaklaşık 93° feather konumuna gider ve Power Lever yok sayılır. Böylece model, pervanenin sürüklemeyi azaltacak şekilde hava akışına paralel hâle getirilmesini görsel olarak gösterir.

Gerçek C-130 Condition Lever açıklamasında FEATHER konumuna çekildiğinde mekanik bağlantıların engine-mounted coordinator üzerinden pervaneye ve engine fuel control shutoff valve'a hareket ilettiği; pervaneye mekanik ve elektriksel feather sinyali verildiği belirtilir. ([Uniforce-SOG][4])

<!-- VİDEO TUTUCU: C-130 Motor Kapatma ve Feather
     Açıklama: Gerçek C-130 kokpitinde condition lever FEATHER konumuna çekilmesi ve pervane bayraklamasının görüntüsü
     Örnek URL: https://www.youtube.com/watch?v=5wKr6YmzTgM
     SearchKeywords: C-130 condition lever feather engine shutdown cockpit video -->

<!-- DİYAGRAM TUTUCU: Feather Konumu Şematik
     Açıklama: Feather konumunda pal açısı (~90°+), hava akışı yönü ve minimum sürükleme durumunu gösteren kesit diyagram
     SearchKeywords: propeller feather position blade angle cross section airflow diagram -->

---

## NTS: Negative Torque Sensing Sistemi

Feather ve air-start mantığını anlatırken NTS sistemine değinmek gerekir. C-130/T56 sisteminde NTS, negative torque durumunu sınırlamak için kullanılan mekanik bir sinyal sistemidir. Negative torque, pervanenin motoru sürmeye çalıştığı durumda oluşur — yani pervane, motor tarafından döndürülmek yerine rüzgâr veya başka dış etkenlerle motoru döndürmeye başlar. Bu durum giderilmezse ciddi sürükleme oluşturur ve uçağın yaw yapmasına neden olabilir.

Uçuş manuelinde NTS sisteminin reduction gear assembly ve propeller valve housing içinde yer alan mekanizmalarla çalıştığı ve negative torque belirli bir değeri aştığında propeller valve housing bağlantılarını etkilediği açıklanır. ([Uniforce-SOG][4])

NTS sinyali geldiğinde sistem, durumu rahatlatmak için pal açısını artırır (coarser pitch yönüne). Burada önemli bir ayrım vardır: **normal NTS çalışması pervaneyi doğrudan full feather'a kilitlemek anlamına gelmez.** Manuelde normal NTS çalışmasının pervaneyi feather'a "commit" etmediği, ancak arızalı bir NTS sisteminin pervaneyi tamamen feather'a götürebileceği veya engine stall/flameout gibi sonuçlara neden olabileceği belirtilir. ([Uniforce-SOG][4])

Power Lever Flight Idle'ın altına indirildiğinde ise bir cam mekanizması NTS actuator'ı NTS plunger'dan uzaklaştırır ve sistemi devre dışı bırakır. Bu, özellikle yüksek iniş hızlarında throttle reverse tarafına hareket ettirildiğinde pervanenin istenmeyen negative torque sinyali almasını önlemek içindir. ([Uniforce-SOG][4])

Modelde NTS fiziksel olarak uygulanmamıştır. Ancak AIR START sırasında amber LED'in işaret ettiği süreç, gerçek sistemde NTS'in air-start prosedüründe izlenen kritik işaretlerden biri olmasına kavramsal olarak dayandırılabilir. Gerçek C-130 air-start checklist'inde flight engineer'ın NTS action'ı izlemesi ve NTS check light yandığında "NTS" diye çağırması istenir. ([Uniforce-SOG][4])

<!-- DİYAGRAM TUTUCU: NTS Sistem Şematik
     Açıklama: NTS mekanizmasının reduction gear, propeller valve housing ve blade angle feedback döngüsü içindeki yerini gösteren basitleştirilmiş şematik
     SearchKeywords: T56 Negative Torque Sensing NTS system reduction gear propeller schematic -->

---

## GROUND STOP / PROP DEMO Modu

GROUND STOP / PROP DEMO modu, modelde güvenli gösterim için kullanılacak ara moddur. Gerçek C-130/T56 sisteminde GROUND STOP, Condition Lever üzerindeki motor durdurma konumudur. Manuelde engine shutdown sırasında condition lever'ların GROUND STOP konumuna alınması ve fuel flow'un sıfıra düşmesinin gözlenmesi istenir. ([Uniforce-SOG][4])

Modelde bu moda ek olarak PROP DEMO davranışı eklenmiştir. Bu modda DC motor çalıştırılmaz. Power Lever aktif kalır ve yalnızca pal açısı değiştirilir. Böylece izleyen kişi pervane dönmeden pallerin nasıl açı değiştirdiğini net görebilir.

Bu davranış gerçek uçağın birebir karşılığı değildir; eğitim ve güvenli sunum amacıyla eklenmiş bir model davranışıdır. Özellikle mekanik test, servo kalibrasyonu ve pal açısı hareketinin anlatılması için kullanışlıdır.

<!-- GÖRSEL TUTUCU: Fotoğraf / Kısa Video
     Açıklama: PROP DEMO modunda motor döndürülmeden servo ile pal açısı değişiminin gösterimi
     SearchKeywords: propeller pitch change servo demonstration model static -->

---

## RUN Modu ve Toggle Switch Mantığı

Modelde RUN modu için iki farklı çalışma yaklaşımı kullanılmıştır. Bunun için panele küçük bir toggle switch eklenecektir. Bu switch yalnızca RUN modu içindeki PWM–pal açısı eğrisini değiştirecektir. FEATHER, GROUND STOP / PROP DEMO ve AIR START modlarının temel davranışı değişmeyecektir.

Toggle switch iki konumlu olacaktır:

| Konum | Mod Adı | Davranış |
|---|---|---|
| Konum 1 | C-130 / Constant-Speed RUN | Motor PWM sabite yakın, pal açısı Power Lever ile değişir |
| Konum 2 | Genel Turboprop Pitch/RPM Demo RUN | RPM ve pal açısı ters orantılı değişir |

Bu sayede model hem C-130/T56 constant-speed mantığını gösterebilecek hem de genel turboprop eğitim mantığını daha anlaşılır şekilde sunabilecektir.

<!-- GÖRSEL TUTUCU: Fotoğraf
     Açıklama: Panel üzerindeki toggle switch'in yakın çekim görünümü ve mod etiketleri
     SearchKeywords: toggle switch panel mode selector labeled closeup -->

---

## RUN Modu 1: C-130 / Constant-Speed RUN

Bu mod, C-130 ailesindeki constant-speed propeller mantığına daha yakın olacak şekilde kurgulanmıştır. Bu yaklaşımda motor/pervane devri sabite yakın tutulur. Power Lever ileri alındıkça asıl görsel değişim pal açısı tarafında olur.

Mantık şu şekildedir:

1. Power Lever ileri alınır.
2. Model daha fazla güç/tork talebini temsil eder.
3. Pal açısı artar.
4. Motor PWM değeri büyük değişimler yapmak yerine sabite yakın tutulur.

Bu modda temsilî pal açısı geçişi: **0° → 5° → 23° → 35° → 55°**

Bu yaklaşım, C-130/T56 sistemindeki governor mantığını anlatmak için uygundur. Çünkü uçuş aralığında pervane governor sistemi constant RPM'i korumaya çalışır; pal açısı, yakıt akışı ve tork birlikte değişir. C-130 uçuş manueli, Flight Range içinde pervane hızının constant RPM tutulduğunu ve overspeed durumunda pilot valve'ın pal açısını artırarak pervaneyi yavaşlattığını açıklar. ([Uniforce-SOG][4])

<!-- GRAFİK TUTUCU: Constant-Speed RUN — PWM ve Pal Açısı Eğrisi
     Açıklama: Power Lever pozisyonuna karşı motor PWM (neredeyse düz çizgi) ve pal açısı (artan eğri) ilişkisini gösteren çift eksenli çizgi grafik
     Eksenler: X = Power Lever pozisyonu (%) | Y₁ = Motor PWM (%) | Y₂ = Pal açısı (°)
     SearchKeywords: constant speed propeller blade angle vs power lever graph PWM constant -->

---

## RUN Modu 2: Genel Turboprop Pitch/RPM Demo

İkinci RUN mantığı, gerçek C-130 davranışını birebir temsil etmek için değil; genel turboprop ve constant-speed propeller eğitim mantığını daha anlaşılır göstermek için kullanılacaktır.

Bu modda kol ileri alındığında high RPM + low/fine pitch davranışı gösterilir. Kol geri alındığında ise low RPM + high/coarse pitch davranışı gösterilir. Bu ilişki, özellikle pilotun propeller RPM'i ayrı bir prop control lever ile seçebildiği piston motorlu constant-speed propeller sistemlerinde ve bazı turboprop eğitim anlatımlarında daha doğrudan görülür. FAA eğitim materyali low-pitch/high-RPM ayarının takeoff için, daha yüksek pitch ve düşük RPM ayarının uçuş sonrası kullanılabileceğini belirtir. ([Federal Aviation Administration][7])

**Ancak bu mod C-130/T56 sisteminin gerçek flight range davranışı değildir.** C-130'da normal uçuş aralığında Power Lever ileri alındığında "RPM sürekli artar" mantığıyla çalışmak yerine, governor RPM'i sabite yakın tutar ve güç değişimi daha çok tork, yakıt akışı ve pal açısı üzerinden gerçekleşir. Bu nedenle model üzerinde bu mod "C-130 gerçek modu" değil, **Genel Turboprop Pitch/RPM Demo** modu olarak adlandırılmalıdır.

<!-- GRAFİK TUTUCU: Genel Turboprop Demo — RPM ve Pal Açısı Eğrisi
     Açıklama: Bu modda Power Lever ilerledikçe RPM'in arttığını ve pal açısının düştüğünü (veya tersi) gösteren çift eksenli çizgi grafik; Constant-Speed RUN grafiği ile yan yana karşılaştırma
     Eksenler: X = Power Lever pozisyonu (%) | Y₁ = Motor PWM/RPM (%) | Y₂ = Pal açısı (°)
     SearchKeywords: turboprop RPM vs blade pitch general education diagram graph -->

---

## AIR START / UNFEATHER Demo Mantığı

AIR START modu, modelde feather'dan çıkış ve yeniden çalıştırma sürecini görsel olarak temsil edecektir. Gerçek C-130/T56 sisteminde AIR START, Condition Lever'ın yay kuvvetine karşı ileri tutulduğu bir konumdur. Uçuş manuelinde AIR START konumunun RUN ile aynı switch'i kapattığı, ayrıca propeller auxiliary pump'ı çalıştıran ikinci bir switch'i devreye soktuğu ve bunun pervaneyi unfeather etmek için basınç sağladığı açıklanır. Auxiliary pump çalıştığında hidrolik sıvı dome assembly pistonunun arka tarafına yönlendirilerek kanatlar düşük pitch açısına getirilir. ([Uniforce-SOG][4])

Gerçek normal air-start checklist'inde engine shutdown sonrası pervane dönüşünün durmuş olduğu kabul edilen bir hazırlık süreci bulunur. Checklist'te condition lever'ın başlangıçta FEATHER konumunda varsayıldığı, önerilen air-start hızının 180 KIAS veya altı olduğu ve Condition Lever'ın AIR START konumunda tutulup light-off sonrası RUN'a bırakıldığı belirtilir. ([Uniforce-SOG][4])

### Model AIR START Sekansı

<!-- TABLO: AIR START Demo Adım Sırası -->

| Adım | Olay | Pal Açısı | Motor PWM | Amber LED |
|---|---|---|---|---|
| 1 | Başlangıç — pervane feather'da, motor kapalı | 93° (sabit) | 0 | Kapalı |
| 2 | AIR START komutu algılandı | 93° (sabit) | 0 | 2× yanıp söner |
| 3 | Unfeather başlangıcı | 93° → 55° | 0 → düşük | Sürekli yanık |
| 4 | Unfeather devam | 55° → 35° | Düşük → orta-düşük | Sürekli yanık |
| 5 | Light-off temsili / sekans sonu | 35° → 23° | Orta-düşük → orta | Sürekli yanık |
| 6 | AIR START tamamlandı | 23° (sabit) | Orta (sabit) | Söner |
| 7 | Kullanıcı Condition Lever'ı RUN'a alır | 23° (başlangıç) | Power Lever'a bağlı | Kapalı |

Gerçek uçakta AIR START konumu yaylı olduğu için light-off sonrası RUN'a bırakılır. Modelde kullanılan potansiyometre fiziksel olarak kendiliğinden RUN'a dönemediği için bu işlem kullanıcı tarafından manuel yapılacaktır.

<!-- AKIŞ DİYAGRAMI TUTUCU: AIR START Sekans Akışı
     Açıklama: AIR START demo sürecinin adım adım akış diyagramı — başlangıç koşulu, LED sinyali, unfeather geçişleri, motor PWM artışı ve sekans sonu kararı
     SearchKeywords: turboprop air start restart sequence flowchart unfeather steps -->

<!-- VİDEO TUTUCU: C-130 Air Start Prosedürü
     Açıklama: Gerçek veya simülatör ortamında C-130 air start prosedürünün uygulanması
     SearchKeywords: C-130 air start procedure cockpit video inflight restart -->

---

## Yazılım ve Elektronik Tarafındaki Geliştirmeler

Cadly turboprop modelinin temel yapısı, basit bir pervane gösterimi için yeterlidir. Ancak bu projede model, daha öğretici bir demonstratöre dönüştürülmektedir.

Bu amaçla sisteme şu özellikler eklenmektedir:

- Condition Lever ile FEATHER, GROUND STOP / PROP DEMO, RUN ve AIR START davranışları
- Power Lever ile pal açısı ve motor PWM eğrilerinin kontrolü
- Toggle switch ile iki farklı RUN mantığı seçimi
- AIR START için amber LED ile durum gösterimi
- Servo ile pal açısı kontrolü
- DC motor ile pervane dönüşü
- AIR START sırasında yavaş ve lineer unfeather animasyonu
- RUN modunda governor mantığını temsil eden PWM–pal açısı eğrileri

<!-- BLOK DİYAGRAM TUTUCU: Sistem Bağlantı Şeması
     Açıklama: Arduino/mikrodenetleyici merkez olmak üzere potansiyometre (Power Lever), potansiyometre (Condition Lever), toggle switch, servo motor, DC motor (H-bridge üzerinden), amber LED ve güç kaynağı arasındaki bağlantıları gösteren blok diyagram
     SearchKeywords: Arduino servo DC motor H-bridge potentiometer toggle switch LED wiring block diagram -->

---

## Modelin Teknik Sınırlamaları

Bu modelde kullanılan servo açısı, gerçek pervane pal açısı mekanizmasının birebir karşılığı değildir. Motor PWM değeri de gerçek pervane RPM'inin doğrudan karşılığı olarak görülmemelidir.

Gerçek uçakta pervane yükü hava akışına, uçuş hızına, motor torkuna, redüksiyon dişli sistemine, governor davranışına, hydraulic control sistemine, NTS mekanizmasına ve cockpit control logic'e bağlıdır. Modelde bu etkilerin tamamı doğrudan ölçülmez. Bunun yerine yazılım tarafında belirlenen eğrilerle görsel ve eğitsel bir temsil oluşturulur.

Bu yüzden modelin amacı **operasyonel doğruluk değil, kavramsal doğruluktur**. Yani amaç gerçek uçak gibi çalışmak değil; gerçek sistemde ne olduğunu anlaşılır şekilde göstermektir.

---

## Sonuç

C-130 ailesi, turboprop motor-pervane ilişkisini anlamak için güçlü bir örnektir. Klasik T56/54H60 sistemi single-shaft turboprop, mechanical/hydraulic governor, Condition Lever ve NTS mantığını temsil ederken, R391 gibi modern pervaneler hydraulic constant-speed, reversible ve full-feathering kabiliyetlerini daha gelişmiş bir yapıda sunar.

Bu projede kullanılan Cadly turboprop 3D modeli, yazılım ve elektronik eklemelerle daha teknik bir demonstratöre dönüştürülmektedir. AIR START animasyonu, toggle switch ile seçilebilen iki farklı RUN mantığı, FEATHER ve GROUND STOP / PROP DEMO modları sayesinde model hem R391 görselliğine hem de C-130 ailesindeki turboprop pervane kontrol mantığına daha anlaşılır bir yapı kazandırmaktadır.

Sonuç olarak bu demonstratör, C-130J/R391 veya T56/54H60 sistemlerinin birebir kopyası değildir. Bunun yerine bu sistemlerdeki temel kavramları görsel olarak anlatan, teknik sunumlarda kullanılabilecek öğretici bir modeldir.

---

## Kaynaklar

1. Rolls-Royce — T56 resmi sayfası: single shaft, modular design turboprop yapısı; 14 kademeli aksiyel kompresör, 4 kademeli türbin ve iki kademeli redüksiyon dişli kutusu bilgileri. ([Rolls-Royce][1])

2. Rolls-Royce — AE2100 resmi sayfası: AE2100D3 motorunun C-130J ve LM-100J platformlarında kullanımı. ([Rolls-Royce][2])

3. Smithsonian National Air and Space Museum — Dowty R391 pervanesinin hydraulic constant-speed, reversible ve full-feathering özellikleri; altı kompozit pal ve 4,115 m çap bilgisi. ([National Air and Space Museum][3])

4. C-130 Flight Manual, CGTO 1C-130-1 — Condition Lever konumları, RUN/AIR START/GROUND STOP/FEATHER işlevleri, propeller speed control system, low pitch stop, NTS sistemi ve air-start checklist detayları. ([Uniforce-SOG][4])

5. Lockheed Martin Service News — T56 100% motor devri 13.820 RPM, 13.54:1 redüksiyon oranı ve yaklaşık 1021 RPM pervane devri bilgisi. ([Lockheed Martin][5])

6. UK CAA / EASA — R391 Type Certificate Data Sheet: variable-pitch, constant-speeding, feathering ve reversing tip; beta control, hydraulic control, counterweights, C-130J/LM-100J kullanımı ve 1020,7 RPM değerleri. ([CAA][6])

7. FAA Aviation Maintenance Technician Handbook, Chapter 7 — Genel constant-speed propeller eğitiminde low-pitch/high-RPM takeoff ve higher-pitch/lower-RPM uçuş sonrası kullanım mantığı. ([Federal Aviation Administration][7])

8. AFMAN 11-2C-130H Vol. 3 — Güncel C-130H operasyonel dokümanında engine shutdown sırasında Condition Lever – GROUND STOP kullanımı. ([E-Publishing][8])

[1]: https://www.rolls-royce.com/products-and-services/defence/aerospace/transport-tanker-patrol-and-tactical/t56.aspx "T56 | Rolls-Royce"
[2]: https://www.rolls-royce.com/products-and-services/defence/aerospace/transport-tanker-patrol-and-tactical/ae-2100.aspx "AE 2100 | Rolls-Royce"
[3]: https://airandspace.si.edu/collection-objects/propeller-variable-pitch-6-blade-dowty-r391/nasm_A20070022000 "Propeller, Variable-Pitch, 6-blade, Dowty R391 | National Air and Space Museum"
[4]: https://uniforce-sog.org/wp-content/uploads/2024/07/USCG-Lockheed-C-130-Flight-Manual.pdf "1C-130-1"
[5]: https://www.lockheedmartin.com/content/dam/lockheed-martin/aero/documents/sustainment/csc/service-news/sn-mag-v11-v20/V16N1.pdf "V16N1.pdf"
[6]: https://www.caa.co.uk/Documents/Download/3940/77d2f18a-4292-443a-8980-607aade5d45a/1112 "R391 TCDS"
[7]: https://www.faa.gov/sites/faa.gov/files/09_amtp_ch7.pdf "Chapter 7 - Propellers"
[8]: https://static.e-publishing.af.mil/production/1/af_a3/publication/afman11-2c-130hv3/afman11-2c-130hv3.pdf "AFMAN11-2C-130HV3"
