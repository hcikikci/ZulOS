# İşletim sistemi örnekleri ve ZulOS fikir havuzu

İlk kayıt: 7 Ekim 2026. Son güncelleme: 8 Ekim 2026.

Bu belge, başlangıç görüşmelerinde ele aldığımız örnekleri ve önerileri toplar. Teknik özellikler bağlantı verilen resmi kaynaklara dayanır. ZulOS'a çıkarılan dersler ve özellik fikirleri tasarım yorumlarıdır.

Kesinleşen kararlar [karar günlüğünde](kararlar.md) tutulur. Buradaki öneriler henüz seçilmiş mimari veya geliştirme taahhüdü değildir. Bazı fikirlerin benzerleri mevcut ürünlerde bulunabilir; bunları tamamen yeni buluşlar olarak sunmuyoruz.

## Bilinen işletim sistemlerinden örnekler

| Örnek | İncelemeye değer yaklaşım | ZulOS için tartışma konusu |
| --- | --- | --- |
| Windows | Kullanıcı alanı ve çekirdek alanı ayrımı; uygulamaların ayrı sanal bellek alanları. | Bir uygulamanın hatasının diğer uygulamalara yayılmasını nasıl önleriz? |
| Linux | Uygulamaların sistem çağrıları ve tanımlı arayüzler üzerinden çekirdek hizmetlerine erişmesi. | Çekirdeğin sunduğu hizmetleri küçük ve anlaşılır nasıl tasarlarız? |
| macOS / XNU | Mach, BSD bileşenleri ve IOKit sürücü altyapısını birleştiren çekirdek. | Farklı tasarım yaklaşımlarını hangi ihtiyaçlar için birleştiririz? |
| Android | Uygulamaları ayrı süreçler ve kullanıcı kimlikleriyle izole eden erişim modeli. | AI dahil her uygulamaya yalnızca ihtiyacı olan erişimi nasıl veririz? |
| ChromeOS | Doğrulanmış açılış ve sistem bütünlüğü üzerinden kurtarma yaklaşımı. | Sistem bozulduğunda güvenilir bir duruma nasıl döneriz? |
| NixOS | İstenen sistem yapılandırmasını tarif etme ve önceki yapılandırma nesillerine dönme. | Ayar değişikliklerini nasıl denenebilir ve geri alınabilir hale getiririz? |
| Redox | Rust ile geliştirilen, mikroçekirdek mimarisi kullanan işletim sistemi. | Çekirdekte hangi sorumluluklar kalmalı, hangileri ayrı hizmetler olmalı? |

Linux bir çekirdektir; Ubuntu ve Fedora gibi dağıtımlar bu çekirdeği kullanıcı araçları ve diğer sistem bileşenleriyle bir araya getirir. Bu örneklerden esinlenmek, onların mimarisini ZulOS için seçtiğimiz anlamına gelmez.

### Resmi kaynaklar

- [Windows: kullanıcı alanı ve çekirdek alanı](https://learn.microsoft.com/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)
- [Linux: kullanıcı alanı API kılavuzu](https://docs.kernel.org/userspace-api/index.html)
- [Apple: XNU kaynak deposu](https://github.com/apple-oss-distributions/xnu/blob/main/README.md)
- [Android: uygulama izolasyonu](https://source.android.com/docs/security/app-sandbox)
- [ChromeOS: güvenlik mimarisi](https://new.chromium.org/chromium-os/developer-library/reference/security/security-whitepaper/)
- [NixOS kılavuzu](https://nixos.org/manual/nixos/stable/)
- [Redox kaynak deposu](https://github.com/redox-os/redox/blob/master/README.md)

## Kişisel asistan deneyimi için fikirler

Bu fikirler, onaylanan kişisel asistan vizyonunu somutlaştırmak için önerildi. Hangi özelliklerle başlayacağımız henüz seçilmedi.

### Kaldığın yerden devam etmek

Asistan üzerinde çalıştığın işi, ilgili dosyaları ve yarım kalan adımları hatırlayabilir. "Devam edelim" dediğinde hangi işi kastettiğini mevcut bağlamdan çıkarabilir.

Bir çalışma alanında dosyalar, terminal, notlar ve açık işler birlikte tutulabilir. Alanı yeniden açtığında çalışma bağlamı geri gelebilir.

### İhtiyaç doğmadan hazırlık yapmak

Yaklaşan toplantı için ilgili notları hazırlamak veya yolculuk öncesinde gerekli belgeleri erişilebilir hale getirmek gibi senaryolar düşünülebilir. Asistan hangi hazırlıkları faydalı bulduğunu zamanla öğrenebilir.

Bu senaryoların gerektirdiği veri kaynakları ve erişimler ayrıca tasarlanacak.

### Kısa ve eksik ifadelerden niyeti anlamak

"Geçen gün baktığımız şeyi aç" gibi bir ifadeyi, izin verilen geçmiş ve mevcut bağlamla ilişkilendirebilir. Belirsizlik yüksek olduğunda kısa bir soruyla netleştirebilir.

Hedef, her iş için uzun ve ayrıntılı talimat verme ihtiyacını azaltmak.

### Kişiye göre davranmak

Bildirim zamanını, önerilerin ayrıntısını ve yardım sıklığını kişinin tercihlerine göre ayarlayabilir. Odaklanırken sessizleşebilir; destek gerektiğinde daha görünür olabilir.

Temel tasarım sorusu: Ne zaman harekete geçmeli, ne zaman öneri sunmalı, ne zaman kullanıcıyı rahat bırakmalı?

### Yetki verilen rutinleri üstlenmek

Tekrarlanan işleri takip edip gerçekleştirebilir. Kullanıcının aynı talimatları her seferinde yeniden vermesi gerekmeyebilir.

Hangi rutinlerin hangi yetkilerle yürütüleceği ve durdurulacağı açık bir tasarım konusu.

### Kullanıcının yönettiği hafıza

Kullanıcı asistanın öğrendiği tercihleri görebilir, düzeltebilir ve silebilir. "Bunu artık yapmıyorum" dediğinde eski alışkanlığa göre davranmayı bırakabilir.

Belirli bir projeye verilen erişimin sınırları ve oturum sonunda unutulacak bağlam ayrıca tasarlanabilir.

### İşlemin planını ve sonucunu görünür kılmak

"İndirilenler klasörünü düzenle" gibi bir işte hangi dosyanın nereye taşınacağı gösterilebilir. Uygun yerel işlemler için geri alma kaydı tutulabilir.

Bu yaklaşım her işte onay istemek olarak kararlaştırılmadı. İnisiyatif düzeyi ve yetki modeli açık konular. Gönderilmiş bir mesaj gibi dış dünyaya ulaşan işlemler her zaman geri alınamaz.

### Kaynak kullanımını anlamak

"Bilgisayar neden yavaş?" sorusuna gerçek işlemci ve bellek ölçümlerinden hareketle cevap verilebilir. İyileştirme önerileri bu ölçümlere dayanabilir.

Önce ölçüm altyapısının kurulması, daha sonra AI açıklamalarının eklenmesi önerildi.

## Teknik tasarımın güncel durumu

8 Ekim 2026 tarihinde mikroçekirdek mimarisi seçildi. Küçük bir çekirdek ve kullanıcı alanında ayrı sistem hizmetleri hedefliyoruz. Kişisel asistanın kullanıcı alanında çalışması bu yönün bir parçası; hizmetin ayrıntılı tasarımı açık.

Aşağıdaki konular hâlâ öneri ve değerlendirme aşamasında:

- AI'ın sistem hizmetlerine tanımlı arayüzlerle ve sınırlı yetkilerle erişmesi.
- Temel sistemin AI kapalıyken de açılıp çalışabilmesi.
- İlk çekirdekten itibaren geliştirmeyi destekleyen olay kayıtları ve ölçümler tutulması.

Bu ayrıntılar henüz onaylanmış kararlar değil. Olay kayıtları geliştirme ve doğrulama için düşünülebilir; "çalışmasını anlatan sistem" ürünün ana yönü olarak benimsenmedi.

## Onaylanan başlangıç ortamı

İlk çekirdeği x86_64 hedefinde QEMU'da çalıştıracağız. QEMU, işlemciyi, belleği ve cihazları kapsayan bir makine modeli sunar. [QEMU belgeleri](https://www.qemu.org/docs/master/about/)

İlk somut hedef açılan ve ekrana çıktı verebilen bir çekirdek. Bunun başarılması, kişisel asistan özelliklerinin veya fiziksel bilgisayar desteğinin hazır olduğu anlamına gelmeyecek.
