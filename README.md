# ZulOS

ZulOS, bilgisayarlar için sıfırdan geliştireceğimiz, kişisel asistan olarak çalışan AI destekli bir işletim sistemi.

Seni tanıyacak, ihtiyaçlarını sezecek, alışkanlıklarına uyum sağlayacak ve hayatını kolaylaştıracak. "Leb demeden leblebiyi anlamak" istediğimiz deneyimi anlatıyor: her seferinde uzun talimatlar vermek zorunda kalmadan, bağlamını anlayan ve zamanla sana uyum sağlayan bir sistem.

Hedef kitle herkes. ZulOS'un kişinin kendi çalışma biçimine ve günlük hayatına uyum sağlamasını istiyoruz.

Geliştirirken gerçek bir işletim sisteminin nasıl çalıştığını da öğreneceğiz. Bu öğrenme süreci, projeyi geliştirme yaklaşımımızın parçası.

Önce temel sistemi kuracağız. AI yeteneklerini bu temelin üzerine, somut ihtiyaçları çözmek için ekleyeceğiz.

## Şu an neredeyiz?

Proje başlangıç aşamasında. Henüz çalışan bir çekirdek veya açılabilir sistem imajı yok.

Onaylanan başlangıç hedefi **x86_64** mimarisi ve **QEMU** geliştirme ortamı. İlk çekirdeği QEMU'da açıp ekrana çıktı verebilir hale getireceğiz.

Programlama dili, önyükleme yaklaşımı ve çekirdek tasarımı henüz seçilmedi. Bunları nedenleri ve alternatifleriyle birlikte değerlendireceğiz. Fiziksel bilgisayarda çalışma, ayrıca donanım ve sürücü desteği gerektiren sonraki bir aşama.

## Vizyon ve tasarım notları

- [Kesinleşen kararlar ve açık konular](docs/kararlar.md)
- [İşletim sistemi örnekleri ve fikir havuzu](docs/fikirler-ve-ornekler.md)

Bu belgeler 7 Ekim 2026 tarihine kadar yaptığımız görüşmelerin özetidir. Fikir havuzundaki özellikler tasarım önerileri; henüz çalışan özellikler veya kesinleşmiş geliştirme taahhütleri değil.

## Nasıl ilerleyeceğiz?

Her adımda üç soruya cevap arayacağız:

- Bu parça gerçek bir işletim sisteminde ne yapıyor?
- ZulOS'ta bunu nasıl gerçekleştireceğiz?
- Çalıştığını nasıl göstereceğiz?

Kararlarımızı, deneylerimizi ve öğrendiklerimizi kodla birlikte bu depoda tutacağız. Çalışan özelliklerle gelecek fikirlerini açıkça ayıracağız.

## İlk yol haritası taslağı

Bu sıra bir başlangıç önerisi; teknik kararlar netleştikçe güncellenecek.

1. **İlk açılış:** Programlama dili ve önyükleme yaklaşımını seçmek; x86_64 hedefinde QEMU'da açılan, ekrana basit bir çıktı üreten ilk çekirdeği çalıştırmak.
2. **Donanımla iletişim:** Temel giriş/çıkış, kesmeler ve zamanlayıcıları öğrenmek.
3. **Bellek:** Bellek yönetimini ve adres alanlarını kurmak.
4. **Program çalıştırma:** Görevler, zamanlama, kullanıcı alanı ve sistem çağrıları üzerinde ilerlemek.
5. **Kullanılabilir temel:** Dosya sistemi, basit bir kabuk ve ihtiyaç duyulan sürücüleri geliştirmek.
6. **Kişisel asistan deneyimi:** Temel sistem çalıştıktan sonra bağlamı anlama, kişiye uyum sağlama ve günlük işleri kolaylaştırma fikirlerini denemek. Erişim, gizlilik, hafıza ve kullanıcı kontrolü bu deneyimin tasarım konuları.

## İlk somut hedef

QEMU'da x86_64 ZulOS çekirdeğini başlatmak ve ekrana ilk çıktısını vermek. Açılışın nasıl gerçekleştiğini öğrenmek ve sonucu tekrar üretebilmek istiyoruz.

Kurulum ve çalıştırma talimatları, ilk çalışan örnekle birlikte eklenecek.

## Lisans

Lisans henüz seçilmedi.
