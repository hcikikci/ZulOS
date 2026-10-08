# ZulOS karar günlüğü

Başlangıç görüşmeleri: 7 Ekim 2026. Son güncelleme: 8 Ekim 2026.

Bu belge, başlangıç görüşmelerinde kesinleşen kararları ve açık kalan konuları kaydeder. Bir önerinin burada açık konu olarak bulunması, uygulanmasına karar verildiği anlamına gelmez.

## Kesinleşen kararlar

| Konu | Karar | Anlamı |
| --- | --- | --- |
| İsim | ZulOS | Projenin adı. |
| Geliştirme yaklaşımı | Sıfırdan işletim sistemi geliştirmek; temellerden başlamak | Kendi çekirdeğimizi geliştirerek ilerleyeceğiz. |
| Ürün vizyonu | Kişisel asistan olarak çalışan AI destekli işletim sistemi | Kullanıcıyı tanıyan, ihtiyaçlarını sezen, uyum sağlayan ve hayatını kolaylaştıran bir deneyim hedefliyoruz. |
| Hedef kitle | Herkes | Ürünün hedef kitlesi belirli bir meslek veya kullanıcı grubuyla sınırlandırılmadı. |
| Hedef cihaz | Bilgisayar | Başlangıçta masaüstü ve dizüstü bilgisayarlar için geliştireceğiz. |
| İlk işlemci mimarisi | x86_64 | İlk hedefimiz 64 bit Intel/AMD PC mimarisi. |
| İlk geliştirme ve çalıştırma ortamı | QEMU | İlk çekirdeği emüle edilen bir bilgisayarda çalıştıracağız. |
| Çekirdeğin ilk deneme dili | Rust | İlk denemeyi Rust ile yapacağız; geliştirme deneyimimize göre seçimi yeniden değerlendirebiliriz. |
| İlk önyükleyici | Limine | Hazır önyükleyiciyle Rust çekirdeğini başlatacağız; Limine'ın nasıl çalıştığını da öğreneceğiz. |
| İlk firmware türü | UEFI | 8 Ekim 2026 tarihinde ilk açılışın UEFI üzerinden yapılması onaylandı; QEMU'daki UEFI ortamını OVMF sağlayacak. |
| Çekirdek mimarisi | Mikroçekirdek | 8 Ekim 2026 tarihinde seçildi. Küçük bir çekirdek ve kullanıcı alanında ayrı sistem hizmetleri hedefliyoruz; ayrıntılı hizmet sınırları ve IPC tasarımı açık. |
| İlk somut hedef | Açılan ve ekrana çıktı verebilen çekirdek | Kişisel asistan deneyiminin üzerine kurulacağı küçük bir temel oluşturacağız. |
| Depo görünürlüğü | Public | Geliştirme ve öğrenme süreci GitHub'da herkese açık. |

## Vizyonun netleştirilmesi

Kullanıcının tarifi:

> Kişisel asistan olarak çalışan bir işletim sistemi olarak düşünmek lazım. Sen leb demeden leblebiyi anlayacak. Seni tanıyacak ve uyum sağlayıp hayatını kolaylaştıracak.

"Çalışmasını anlatan işletim sistemi" fikri ürünün ana yönü olarak benimsenmedi. İşletim sistemi geliştirmeyi öğrenmek bizim geliştirme sürecimizin bir parçası; ürünün merkezinde kişisel asistan deneyimi var.

Bir bilgisayarı ve x86_64 + QEMU ortamını başlangıç hedefi olarak seçmek, hedef kitleyi değiştirmiyor. Geliştirmeye başlayacağımız teknik ortamı belirliyor.

## Açık konular

- Rust sürümü, derleme araçları ve geliştirme ortamının kurulumu.
- İlk Rust denemesinden sonra dil seçiminin değerlendirilmesi.
- Limine sürümü, protokol revizyonu ve kullanılacak OVMF paketi/sürümü.
- Açılış, kurtarma ve güncelleme deneyimine hangi ZulOS özelliklerinin ekleneceği.
- Mikroçekirdeğin ayrıntılı sorumlulukları ve sistem hizmetlerinin sınırları.
- Süreçler arası iletişim (IPC), hizmetlere erişim ve mesajların işlenme modeli.
- İlk kullanıcı alanı hizmetinin başlatılması ve hizmet hatalarından toparlanma yaklaşımı.
- Fiziksel bilgisayarlarda ilk desteklenecek donanım ve sürücüler.
- İlk kişisel asistan senaryosu ve nasıl değerlendirileceği.
- AI'ın sistemle nasıl iletişim kuracağı ve hangi yetkilere sahip olacağı.
- Kullanıcı hafızası, gizlilik, yerel model ve bulut modeli tercihleri.
- Asistanın hangi işlerde kendiliğinden hareket edeceği, hangilerinde öneri sunacağı.
- Lisans seçimi.

Bu konuları sırayla ele alacağız. Mimari ve özellik önerileri [fikir havuzunda](fikirler-ve-ornekler.md) duruyor.

Limine'ın görevi ve açılışta geliştirebileceğimiz fikirler [önyükleme notlarında](onyukleme.md) açıklanıyor. Limine seçimi, bu fikirlerin uygulanmasına karar verildiği anlamına gelmiyor.

## Mevcut durum

Depoda başlangıç belgeleri var. Henüz çalışan çekirdek, açılabilir sistem imajı, AI hizmeti veya kurulum talimatı yok. QEMU'da veya fiziksel bilgisayarda bir çalışma doğrulaması henüz yapılmadı.
