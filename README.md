# ZulOS

ZulOS, bilgisayarlar için sıfırdan geliştireceğimiz, kişisel asistan olarak çalışan AI destekli bir işletim sistemi.

Seni tanıyacak, ihtiyaçlarını sezecek, alışkanlıklarına uyum sağlayacak ve hayatını kolaylaştıracak. "Leb demeden leblebiyi anlamak" istediğimiz deneyimi anlatıyor: her seferinde uzun talimatlar vermek zorunda kalmadan, bağlamını anlayan ve zamanla sana uyum sağlayan bir sistem.

Hedef kitle herkes. ZulOS'un kişinin kendi çalışma biçimine ve günlük hayatına uyum sağlamasını istiyoruz.

Geliştirirken gerçek bir işletim sisteminin nasıl çalıştığını da öğreneceğiz. Bu öğrenme süreci, projeyi geliştirme yaklaşımımızın parçası.

Önce temel sistemi kuracağız. AI yeteneklerini bu temelin üzerine, somut ihtiyaçları çözmek için ekleyeceğiz.

## Şu an neredeyiz?

Proje başlangıç aşamasında. Henüz çalışan bir çekirdek veya açılabilir sistem imajı yok.

Onaylanan başlangıç hedefi **x86_64** mimarisi ve **QEMU** geliştirme ortamı. İlk çekirdeği QEMU'da açıp ekrana çıktı verebilir hale getireceğiz.

Çekirdeğin ilk deneme dili **Rust** olarak seçildi. İlk geliştirme deneyimimizden sonra bu seçimi yeniden değerlendirebiliriz.

İlk açılış için **Limine** önyükleyicisini kullanacağız. [Önyükleme notları](docs/onyukleme.md), bu parçanın ne yaptığını ve ZulOS'un açılış zincirini açıklıyor.

İlk açılış **UEFI** üzerinden olacak. QEMU'daki UEFI ortamını **OVMF** sağlayacak: QEMU → OVMF/UEFI → Limine → ZulOS Rust çekirdeği.

Çekirdek mimarisi **mikroçekirdek** olarak seçildi. Çekirdeği küçük tutup sürücüler, dosya sistemi ve kişisel asistan gibi işlevleri kullanıcı alanındaki ayrı hizmetlerde geliştirmeyi hedefliyoruz. Ayrıntılı hizmet sınırları ve süreçler arası iletişim (IPC) tasarımı henüz seçilmedi.

Limine sürümü, protokol revizyonu ve geliştirme araçları henüz seçilmedi. Bunları nedenleri ve alternatifleriyle birlikte değerlendireceğiz. Fiziksel bilgisayarda çalışma, ayrıca donanım ve sürücü desteği gerektiren sonraki bir aşama.

## Mikroçekirdek yönü

Başlangıç sorumluluk ayrımı taslağı:

- **Çekirdek:** Görevlerin çalıştırılması, adres alanlarının korunması, temel kesme ve donanım erişim mekanizmaları, hizmetlerin iletişim kuracağı IPC altyapısı.
- **Kullanıcı alanı:** Sürücü hizmetleri, dosya sistemi, ağ, masaüstü ve kişisel asistan.

Bu ayrımın amacı hizmetleri birbirinden izole edebilmek. Bir hizmetin yeniden başlatılması, ona bağlı işlerin toparlanması ve erişim kuralları ayrıca tasarlanacak; mikroçekirdek seçimi tek başına bunları gerçekleştirmez.

## Vizyon ve tasarım notları

- [Kesinleşen kararlar ve açık konular](docs/kararlar.md)
- [İşletim sistemi örnekleri ve fikir havuzu](docs/fikirler-ve-ornekler.md)
- [Bootloader ve Limine nasıl çalışır?](docs/onyukleme.md)

Bu belgeler 8 Ekim 2026 tarihine kadar yaptığımız görüşmelerin özetidir. Fikir havuzundaki özellikler tasarım önerileri; henüz çalışan özellikler veya kesinleşmiş geliştirme taahhütleri değil.

## Nasıl ilerleyeceğiz?

Her adımda üç soruya cevap arayacağız:

- Bu parça gerçek bir işletim sisteminde ne yapıyor?
- ZulOS'ta bunu nasıl gerçekleştireceğiz?
- Çalıştığını nasıl göstereceğiz?

Kararlarımızı, deneylerimizi ve öğrendiklerimizi kodla birlikte bu depoda tutacağız. Çalışan özelliklerle gelecek fikirlerini açıkça ayıracağız.

## İlk yol haritası taslağı

Bu sıra bir başlangıç önerisi; teknik kararlar netleştikçe güncellenecek.

1. **İlk açılış:** Sürümleri ve araçları seçmek; UEFI/OVMF ortamında Limine ile başlatılan Rust çekirdeğini x86_64 hedefinde QEMU'da çalıştırmak ve ekrana basit bir çıktı vermek.
2. **Donanımla iletişim:** Temel giriş/çıkış, kesmeler ve zamanlayıcıları öğrenmek.
3. **Bellek:** Bellek yönetimini ve adres alanlarını kurmak.
4. **Kullanıcı alanı ve iletişim:** Görevler, zamanlama, sistem çağrıları ve IPC üzerinde ilerlemek; ayrı adres alanlarında çalışan iki hizmetin mesaj alışverişini göstermek.
5. **Kullanılabilir temel:** Dosya sistemi ve ihtiyaç duyulan sürücüleri kullanıcı alanındaki hizmetler olarak geliştirmek; basit bir kabuk eklemek.
6. **Kişisel asistan deneyimi:** Temel sistem çalıştıktan sonra bağlamı anlama, kişiye uyum sağlama ve günlük işleri kolaylaştırma fikirlerini denemek. Erişim, gizlilik, hafıza ve kullanıcı kontrolü bu deneyimin tasarım konuları.

## İlk somut hedef

QEMU'da x86_64 ZulOS çekirdeğini başlatmak ve ekrana ilk çıktısını vermek. Açılışın nasıl gerçekleştiğini öğrenmek ve sonucu tekrar üretebilmek istiyoruz.

İlk açılış çıktısı bir başlangıç deneyi olacak. Mikroçekirdek ayrımını çalışan bir sistemde göstermek için daha sonra kullanıcı alanı izolasyonunu ve hizmetler arası iletişimi gerçekleştireceğiz.

Kurulum ve çalıştırma talimatları, ilk çalışan örnekle birlikte eklenecek.

## Lisans

Lisans henüz seçilmedi.
