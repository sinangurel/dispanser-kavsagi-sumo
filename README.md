# Dispanser Kavşağı — Uyarlamalı Sinyal Kontrolü

## Amaç
Kırıkkale Dispanser Kavşağı’nın saha verisine dayalı SUMO modelini oluşturmak; sabit süreli ve uyarlamalı sinyal planlarını aynı trafik talebi ve rastgele tohumlarla karşılaştırmak.

## Mevcut durum
- SUMO kurulup çalıştırıldı.
- İlk kavşak modeli oluşturuldu ve yol bağlantıları gözlemlere göre düzeltildi.
- Model ve sentetik deneme trafiği `Dispanser_v3/` klasörüne eklendi.
- Saha araç sayımı ve gerçek sinyal süresi ölçümleri henüz yapılmadı.
- Modelin saha doğrulaması ve uyarlamalı kontrol algoritması henüz tamamlanmadı.

Mevcut model şematiktir. Deneme trafiği gerçek saha sayımı değildir.

## Başarı ölçütü
- Ortalama gecikme: saniye/araç.
- Kuyruk uzunluğu: araç sayısı.
- Hedef fark: ___
- Ölçülmüş karşılaştırma sonucu: ___

Gecikme tanımı ve kuyruk ölçüm yöntemi karşılaştırmalardan önce belirlenecektir.

## Kavşak düzeni
Üstten gelen yol yalnızca kavşağa giriş yönündedir. Erken sağa ayrılan kolun ayrı ışığı vardır. Kavşak içinden sağ alttaki yola devam edilebilir. Sağ alttaki yoldan kavşağa giriş ışıkla kontrol edilir.

- Saha krokisi: henüz eklenmedi.
- Kol ve şerit bilgileri: sahada doğrulanacak.
- İzin verilen dönüşler: sahada doğrulanacak.
- Üç döngülük faz süresi tablosu: henüz ölçülmedi.
- Model dosyası: `Dispanser_v3/kavsak_v3.net.xml`

Modeldeki ışık süreleri geçici deneme değerleridir.

## Veri toplama
İlk saha çalışmasında:
- Kavşak kolları, şeritler, dönüşler ve yaya geçitleri gözlenecek.
- Sinyal gruplarının faz sırası ve süreleri üç döngü boyunca kaydedilecek.
- Tek giriş kolunda 15 dakikalık deneme sayımı yapılacak.
- Sayımlar 5 dakikalık aralıklarda; yön ve araç türüne göre tutulacak.

Ölçüm tarihi: ___  
Seçilen kol: ___  
Başlangıç–bitiş saati: ___  
Gözlem sorunları: ___

Eksik ölçümler sıfır olarak yazılmayacaktır. Tek koldaki deneme sayımı tüm kavşağı temsil ediyor kabul edilmeyecektir.

## Blok şema
Saha krokisi → SUMO yol ağı  
Saha sayımı → talep/rota dosyası  
Ölçülen faz süreleri → sabit süreli referans plan  

SUMO ağı + aynı talep ve rastgele tohumlar  
→ sabit süreli plan / en az–en çok yeşil sınırları olan uyarlamalı denetleyici (Python–TraCI)  
→ ortalama gecikme ve kuyruk uzunluğu ölçümü  
→ saha verisiyle doğrulama ve yöntemlerin karşılaştırılması

Modeli ayarlamak ve doğrulamak için kullanılacak ölçümler ayrılacaktır.

## Hesaplama ortamı
- İşletim sistemi: ___
- SUMO sürümü: ___
- Python sürümü: ___
- Python–SUMO bağlantısı: `traci`
- Diğer paketler: ___

## Çalıştırma
1. Depoyu indirip ZIP içeriğini bir klasöre çıkar.
2. SUMO-GUI programını aç.
3. File → Open Simulation menüsünden `Dispanser_v3/deneme.sumocfg` dosyasını seç.
4. Oynat düğmesine bas.

Yol ağını düzenlemek için NETEDIT ile `Dispanser_v3/kavsak_v3.net.xml` dosyasını aç.

## Klasör yapısı
- `Dispanser_v3/`: mevcut ağ, düzenlenebilir kaynaklar ve sentetik deneme dosyaları.
- `data/`: saha krokisi, sayım formları ve faz ölçümleri için oluşturulacak.
- `scripts/`: kontrol ve analiz kodları için oluşturulacak.
- `results/`: sonuç tabloları ve grafikler için oluşturulacak.

## Ortam kontrolü
PowerShell'de şu komutları çalıştır:

- `sumo --version` → SUMO sürüm bilgisi görülmeli.
- `python --version` → Python sürüm bilgisi görülmeli.
- `python -c "import traci; print('TraCI içe aktarma başarılı')"` → başarı mesajı görülmeli.

Komut bulunamazsa ilgili kurulum/PATH ayarı; `ModuleNotFoundError` görülürse kullanılan Python ortamındaki paket erişimi kontrol edilmelidir.

Bu kontroller, modelin saha doğrulamasının yapıldığı anlamına gelmez.

## Sıradaki adım
Saha krokisini tamamlamak, üç döngülük sinyal sürelerini ölçmek ve tek kolda 15 dakikalık deneme sayımını yaparak ham verileri depoya eklemek.
