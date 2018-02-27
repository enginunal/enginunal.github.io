[Ana Sayfa](https://enginunal.github.io/)

# Bulut Mimarisinin Temelleri

## Bulut Bilişim Tipleri

### Özel Bulut (Private Cloud)
Bulut servislerinin kullanıcıya özel olarak sunulmasıdır. Sunulan kaynaklar diğer kullanıcılarla paylaşılmaz, kullanıcı kendisine sunulan bulut servislerinin ölçeklenebilirlik, elastiklik gibi özelliklerini kullanırken kontrol ve uyarlanabilirlik özelliklerine de sahip olur. Özel bulut servisleri IaaS ve Paas modeli ile sağlanabilir. Iaas, Servis Olarak Altyapı(ağ,depolama..) ve PaaS, Servis Olarak Platform(işletim sistemi, web sunucusu, veritabanı sunucusu...) anlamına gelmektedir.  
Dahili veya kurumsal bir bulut olarak da adlandırılan özel bulut, şirketlere barındırılan bilgisayar altyapısı üzerinden özelleştirilmiş kaynaklardan sağlanan ek kontrol ve özelleştirme sayesinde, işletmelerin self-servis, ölçeklenebilirlik(scalability) ve elastikiyet(elasticity) gibi genel bir bulutun pek çok avantajını sağlar

### Genel Bulut (Public Cloud)
Internet üzerindeki sunucular ile sağlanan ve herkese açık olan bulut hizmetidir. Genel bulut, bir hizmet sağlayıcının sanal makineler (VM'ler), uygulamalar veya depolama gibi kaynakları, internet üzerinden herkese açık hale getirdiği standart bulut bilişim modeline dayanır.  
Sunulan hizmetler kullanıcılara ücretsiz veya ücret karşılığı sağlanabilir. Kullandığın kadar öde modeli de uygulanmaktadır.
Özel bulutların aksine, genel bulutlar firmaları şirket içi donanım ve uygulama altyapısı satın almak, yönetmek ve bakım yapmak zorunda kalmaktan kurtarabilir - bulut hizmeti sağlayıcısı sistemin tüm yönetim ve bakımından sorumlu tutulur.

### Melez Bulut (Hybrid Cloud)
Melez bulut, genel bulut ile özel bulut arasında veri ve uygulamaların paylaşılmasını sağlayarak bulut ortamını entegre eder. En kısa ifadeyle, kurum içi kaynakların gelen bulut kaynaklarıyla bütünleştirilmesidir.  
Genellikle, melez bulut, bir genel bulut hizmetinin ve kurum içi bir özel bulutun kombinasyonunu ifade eder; Bununla birlikte, melez bulutlar, farklı sağlayıcılar tarafından sağlanan genel bulutlardan veya bulut ile geleneksel IT'nin bir kombinasyonundan oluşabilir. Aslında, geleneksel IT altyapısında mevcut sistemlerin bir genel bulut hizmeti ile birleştirildiği bir kurulum şu anda hibrit bulutun en yaygın kullanımı halidir.  
Melez bulut kullanmak, yalnızca şirketlerin bilgi işlem kaynaklarını ölçeklendirmesine olanak tanımakla kalmaz aynı zamanda kısa süreli talep artışlarını karşılamak için büyük sermaye harcamaları yapma ihtiyacını ve işin daha hassas veri veya uygulamalar için yerel kaynakları ayırması gereksinimini ortadan kaldırır.


## Genel Bulut Servis Modelleri (Public Cloud Services)

Bu konuyla ilgili aşağıdaki görsel ile başlayalım. IaaS, PaaS ve SaaS ile ilgili olan bu görsel aşağıdaki anlatım öncesi bir fikir verecektir.  

![image](/images/BulutTemelleri/PublicCloudServices.jpg)  


Tek tek IaaS, PaaS ve SaaS maddelerine geçmeden önce konuyu basitleştirmek adına yakın zamanda okuduğum bir yazıdaki örnekle başlamak istiyorum.  
Tek başına, altyapı(IaaS) kullanışlı değildir - orada sadece duran ve birisinin belirli bir sorunun çözümünde üretken olmasını bekleyen bir yapıdan başka birşey değildir. Ülkedeki ulaşım sistemini düşünün. Tüm bu yollar inşa edilmiş olsa bile, insanlar ve eşyaları taşımak için araba ve kamyon olmadan kullanışlı olmazlar. Bu benzetmede, yollar altyapıya(IaaS), arabalar ve kamyonlar ise altyapının üzerine oturan ve insanları ve eşyaları taşıyan platformdur(PaaS). Eşyalar ve insanlar ise teknik alanda yazılım(SaaS) ve bilgi olarak düşünülebilir.

### Servis Olarak Altyapı – IaaS (Infrastructure As A Service)
IaaS, bilgi işlem, depolama, ağ oluşturma ve diğer kabiliyetleri Internet üzerinden sunmanın bir yöntemidir. IaaS, şirketlerin temel bulut altyapısını satın almak, yönetmek ve desteklemek zorunda kalmadan web tabanlı işletim sistemlerini, uygulamaları ve depolamayı kullanmalarını sağlar. IaaS platformlarının en popüler örnekleri Amazon Web Hizmetleri (AWS) ve Microsoft Azure'dur.
Kullanıcılar, genel ortam için bir IT operasyon yönetimi konsolu olarak hizmet veren Web tabanlı bir grafik kullanıcı arayüzü kullanarak, bu altyapıyı kendi başlarına yönetebilirler. Altyapıya API erişimi bir seçenek olarak sunulabilir.  
En kısa ifadeyle IaaS, kullanıcılara depolama, ağ oluşturma, sunuculara ve buluttaki diğer bilgi işlem kaynaklarına ücret karşılığı erişim sağlayan servistir.  
Kullanıcı, kendi ihtiyaçları doğrultusunda CPU, RAM ve Depolama miktarını belirler ve bu özellikleri sağlayan bir VM(virtual machine)’i servis sağlayıcıdan satın alır. Bu VM alındıktan sonraki adımlarda işletim sistemi bakımı ve yönetimi, servis konfigürasyonu kullanıcı tarafından gerçekleştirilir. 

### Servis Olarak Platform – PaaS (Platform As A Service)
PaaS, IaaS’e ek olarak yazılım, geliştirme araçları, iş zekası (BI) hizmetleri, veritabanı yönetim sistemleri gibi sistemler de içerir. Yazılım lisansları, uygulama altyapısı, geliştirme araçları ve diğer kaynakları satın alma ve yönetme zorunluluğundan kurtarır. Bu hizmetler bulut sağlayıcısı tarafından verilmektedir.  
PaaS, geliştiricilerin internet üzerinden uygulamalar ve hizmetler oluşturmasına izin veren bir platform ve ortam sağlar.
PaaS, SaaS'tan daha düşük bir seviyede çalışır ve temel olarak yazılımın geliştirilip dağıtılabileceği bir platform sağlar. PaaS sağlayıcıları, altta yatan sunucu donanım ve ağ altyapısını bakımı ve sunucularla uğraşma zorluğunu üstlenir ve kullanıcılara sadece iş  tarafına odaklanmayı sağlayan bir ortam sunar. 

### Servis Olarak Yazılım – SaaS (Software As A Service)
SaaS, yazılımın bulutta barındığı ve internet üzerinden erişildiği bir abonelik tabanlı modeli ifade eder. Basitçe web veya bir API aracılığıyla erişilen bulut tabanlı uygulamalar olarak tanımlanır.  
Depolama ve işleme işlemlerini bulut sunucularında gerçekleştirilir ve servise erişmek ve kullanmak için oldukça basit ve yaygın bir istemci (genellikle bir web tarayıcısı) kullanılır. Hizmet sağlayıcısı, donanım ve yazılımı yönetir ve hizmet sözleşmesi ile uygulamalarınızın ve verilerinizin kullanılabilirliğini ve güvenliğini sağlar.
Web tabanlı email hizmetleri, sosyal medya, web tabanlı müzik dinleme hizmeti veren uygulamalar SaaS’e örnek olarak verilebilir.

## Konteyner’lar ve MikroServisler (Containers And Microservices)

### Konteyner
Container, bir uygulamanın kodunu, yapılandırmalarını ve bağımlılıklarını, tutarlılık, verimlilik, üretkenlik ve sürüm denetimi için yapı taşları olarak paketleyen bir sanallaştırma(virtualization) yöntemidir. 
Container, yazılımın paylaşılan bir işletim sisteminde izoleli olarak çalışabilen bir biçimde paketlenmesinin bir yoludur. VM'lerin aksine, container bir işletim sistemi paketlemez; yalnızca yazılımı çalıştırmak için gereken kütüphaneler ve ayarlara ihtiyaç vardır. Bu, yazılımın nerede konuşlandırıldığına bakılmaksızın yazılımın daima aynı şekilde çalışacağını garanti eder.  
Container teknolojisi ile uygulamaların deploy edilmesi çok daha kolay ve VM’e göre çok çok hızlıdır. Continuous Integration gibi yazılım geliştirme süreçlerinde geliştiricilerin otomasyona bağladığı derleme ve test süreci sonrasında yayın süreci gelmektedir, yayın(deployment) sürecinin sorunsuz gerçekleşmesi çok önemlidir. Üretilen ve test edilen bir yazılımın kullanıcının deneyimine sunulma aşamasında kullanıcının işlerini kesintiye uğratmadan deployment tamamlanmalı ve bu işlemler hatasız gerçekleşmelidir. Container’lar bu alanda da önemli kolaylık getirmiştir ve kullanımları yaygınlaşmaktadır.  
Konteynerlar bir konteyner engine üzerinde çalışır ve bu container engine aşağıdaki işletim sisteminden bağımsız olarak çalışır, alttaki yapının VM veya fiziksel bir makina olmasının önemi yoktur.   
Konteynerlar için endüstri standardı Docker olarak söylenebilir. Çoğu büyük platform Docker engine desteğine sahiptir ve Docker imajlarını bu engine üzerinde çalıştırmaktadır. Bu imajlara Dockerfile ismi verilir ve Dockerfile içerisinde konfigürasyon tanımları, uygulamalar, servisler vb gerekli tüm şeyler bulunur. 

### MikroServisler ve Konteyner Orkestrasyonu
Diyelim ki uygulamamız büyüyor ve tek bir blok olarak giderek daha fazla fonksiyon eklemeye devam ettik. Uygulama çok fazla CPU ve RAM tüketen ve yönetimi neredeyse imkansız bir hale gelmeye başladı. Bu durumda ne yapmak gerekir?   
Uygulamamızı daha küçük parçalara ayırmaya karar verir ve her biri belirli bir görev veya fonksiyon için sorumlu daha küçük bölümlere yani mikroservislere(microservices) ayırmaya karar veririz.  
İşte bu durumda bir ihtiyaç daha ortaya çıkıyor o da Konteyner Orkestrasyonu(Container Orchestration), konteynerların otomatik olarak düzenlenmesi, koordinasyonu ve yönetimi anlamına gelir. Bir uygulama için bir den çok container kullanılabilir ve bu container’lar arasında uyumun sağlanması için container’ların yönetilmesi, yayınlanması, konfigürasyonu işlemlerinin gerçekleştirilmesi bu şekilde olmaktadır. Örnek tool olarak Kubernetes verilebilir.

## Bulut Kimlik Yönetimi

### Hesap Koruma Yöntemleri
Bulut kaynaklarına erişimde kimlik yönetimi ve kullanılan hesapların koruması önemli konulardan biridir. Örneğin yönetici hesabı tüm kaynaklara, servislere erişim hakkına ve tüm kullanıcıların yetkilerini belirleme onları blok etme hakkına sahiptir ve güvenliği bu nedenle oldukça önemlidir. Bu güvenliği sağlamak için bazı noktalara dikkat etmek gerekir. Bunlar:  

•	Şifre güvenliği  
Şifrelerin tahmin edilememesi için şifre belirlemede akılda kalan veya tahmin edilebilen şifreler yerine içinde büyük küçük harf kombinasyonu ve rakam içeren daha karmaşık şifreler kullanılmalıdır. Brute Force gibi şifre kırma ataklarına karşı güçlü şifrelerin belirlenmesi önemli bir güvenlik konusudur.  

•	Çok faktörlü kimlik doğrulama (Multi Factor Authentication)  
Hesabınıza güvenli bir şekilde erişilmesine yardımcı olmak için kullanılır ve hesaba giriş işlemini her biri farklı bir faktör kategorisinden doğrulayarak kullanıcıyı tanımlama işlemidir.   

•	Koşullu Erişim (Condition Access) ve Sahtekarlığı Algılama(Fraud Detection)  
Koşullu erişim, kullanıcılara konum, aygıt ve uygulama düzeyinde içeriğe dayalı kontroller sağlayan ilkeler tanımlaya imkan veren yöntemdir. Örneğin bir kullanıcının belirlenen IP’ler dışında başka bir IP aralığından bağlanması engellenebilir.
Fraud Detection, sahtekarlık veya hile ile sisteme girmeye çalışanların algılanmasıdır. Örneğin bir kullanıcı kendi hesabına ilk girişi Türkiye,İstanbul’dan yapmış ve bu işlemden beş dakika sonra İngiltere’den giriş yapmaya çalıştığını düşünelim. Bu işlem şüpheli olarak kabul edilip Fraud Detection kuralları ile algılanıp bloklanabilir.  

Yukarıda saydığım güvenlik önlemlerine yenileri de eklenebilir fakat ne kadar önlem alınırsa alınsın bu bir sistemin tamamen güvenli olduğu anlamına gelmez. Her zaman birilerinin bir yöntem veya açık bulup sisteme erişme imkanı olabileceği olasılığı göz ardı edilmemelidir.  
Olası sızmalara veya saldırılara maruz kalınan durumlarda sistemin işleyişinin devamına yönelik de bazı önlemler geliştirilmelidir. Örneğin bir bulut ortamında admin hesabının yaratılan tüm ortam üzerinde tam yetkisi vardır. Uygulamaların ve servislerin tek ortamda olduğunu ve bunun bir admin ile yönetildiğini varsayalım. Admin hesabı ile ilgili bir sorun yaşandığında tüm ortamın çalışamaz hale gelmesi sözkonusudur. Buna karşı uygulamaların ve servislerin farklı ortamlara dağıtılması, birbirini yedeklemesi ve bu ortamların farklı admin hesaplarıyla yönetilmesi daha güvenli olacaktır. Bu şekilde bir hesap ile sorun yaşandığında sistemin diğer ortamlardan ayağa kalkarak devamlılığının sağlanması daha sağlıklı olacaktır.

### Rol Tabanlı Erişim Kontrolü
Rol tabanlı erişim kontrolü (Role Based Access Control - RBAC), kullanıcıların rollerine dayalı olarak bilgisayar veya ağ kaynaklarına erişimi düzenleyen bir yöntemdir. Örneğin bulut sisteminde bir yönetici hesabı ve veritabanı işlemleri yapan başka hesaplar olsun. Tüm bu hesaplara aynı hakları verip tüm kaynaklara erişimi açmak güvenlik riskleri oluşmasına yol açar. Bunun yerine kullanıcılara ve yöneticilere gerektiği kadar ve gereken ölçüde hak verilmeli ve bu hakların sistemde nasıl bir risk oluşturabileceği önceden analiz edilmelidir.

## Sunucusuz Bilgi İşlem (Serverless Computing) (FaaS)

Diğer adıyla Servis Olarak Fonksiyonlar (Functions as a Service - FaaS).   
Öncelikle belirtmek gerekiyor ki bu serverless isimlendirmesi kullanılmasına bakılmaması gerekiyor, çünkü bu konu tamamen serverlar üzerinde geçiyor ve onlara bağımlı. Bu nedenle başlığın verdiği önyargıyı yazının başında kırmak önemli. Serverless programming bulut servis sağlayıcısının sunduğu fonksiyonlar ile gerçekleştiriliyor.   

Önemli üç nokta var:   
•	Sunucuların geliştiriciden tamamen soyutlanması, yani geliştiriciler sunucu ile ilgili herhangi bir bilgiye sahip olmak zorunda değil. Kullanılan altyapı için bir ücretlendirme yok.  
•	Tüketim ve çalıştırma temelli faturalandırma, sunucunun alanı,performansı fiyatta belirleyici değil. Fiyat ne kadar çalıştırıldığı ile ilgili ücretlendirme var.  
•	Olay güdümlü ve anında ölçeklenebilir olan servisler. Bulut platformunun sunduğu fonksiyonlar, API ve hizmetler kullanılıyor. Kodlama olay güdümlü ve stateless yazılıyor. Yazılan kodun verimi ücretlendirmeyi de doğal olarak etkiliyor.  

Olay güdümlü sistemler için yeni bir mimari kalıptan bahsediyoruz. Bu nedenle, sunucu içermeyen işlevler genellikle diğer hizmetler arasında bağlayıcı olarak veya olay odaklı bir mimaride kullanılır. Kısa ömürlüdür, durum bilgisi tutmaz, mevcut hizmetlerinizden veya üçüncü parti kaynaklardan faydalanır, bir kaç saniye içinde işini yapar.  
Sunucusuz bilgi işlem, kod çalıştırma işleminin, geleneksel uygulama geliştirme ve sunuculara dağıtma yöntemi yerine tamamen bir bulut sağlayıcısı tarafından yönetildiği bir mimaridir. Geliştiricilerin, kod dağıtırken sunucuları yönetmek, hazırlamak ve korumak için endişe duymamaları anlamına gelir.  
Daha öncesinde bir geliştirici, ne kadar depolama ve veritabanı kapasitesi gerekiyor bunu tanımlamak zorundaydı ve toplam süreç bu nedenle yavaşlamaktaydı fakat bu yöntemle bu tip endişelere gerek duyulmamaktadır.  

Sunucusuz uygulamalar oluşturmak, uygulama geliştiricilerinin bulut veya lokaldeki sistemin yönetilmesi ve çalıştırılması ile ilgilenmek yerine uygulama geliştirmeye odaklanabileceği anlamına gelir. Bu azaltılmış yük, geliştiricilerin ölçekli ve güvenilir ürünler geliştirmek için daha fazla zaman ve enerjiyi ürüne ayırmalarını sağlar.  
Bu hizmeti veren hizmet sağlayıcıların örnek ürünleri, AWS Lambda, Azure WebJobs, IBM OpenWhisk, Google Cloud Functions olarak sıralanabilir.

