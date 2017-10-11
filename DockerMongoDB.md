# Container Nedir? Docker Nedir? MongoDB Container Kurulum Örneği


Bu yazıda Container konusuna giriş yapıp devamında Docker ve MongoDB document database kullanımını ve bunun docker container olarak lokal makinamıza nasıl kurabileceğimizi kısaca anlatmaya çalışacağım. Öncelikle container nedir? Ne değildir? Buna bir bakıp Docker konusuna geçelim.

## Container


Container, uygulamalarımızı bir yapı içine koyup istediğimiz yere gönderebileceğimiz ve orada bir kurulum/setup ihtiyacı olmadan ve uyumluluk sorunu yaşamadan çalışabilmelerini sağlayan teknolojidir. Bunun tam anlaşılabilmesi için VM(Virtual Machine) ne demek onu da bilmek gerekiyor. VM, sanal makina anlamına gelmekte olup işletim sistemi barındıran yapılar olmakla beraber başlı başına bir bilgisayarı simule eder. Her VM içinde bir işletim sistemi çalışır ki o işletim sistemine RAM ayrılması zorunluluğu doğar. Bu da VM’e ayrılan RAM’den işletim sistemine gidecek bir kaynak demektir.
VM’ler büyük ve hantal yapılardır, deploy(yazılım yayınlama) gereken durumlarda deploy süresi uzun, tükettiği sistem kaynağı fazladır. Bu örnekler çoğaltılabilir. Peki container nedir ne artı getiriyor?

Container, yazılımın paylaşılan bir işletim sisteminde izoleli olarak çalışabilen bir biçimde paketlenmesinin bir yoludur. VM'lerin aksine, container bir işletim sistemi paketlemez; yalnızca yazılımı çalıştırmak için gereken kütüphaneler ve ayarlara ihtiyaç vardır. Bu, yazılımın nerede konuşlandırıldığına bakılmaksızın yazılımın daima aynı şekilde çalışacağını garanti eder.
Container teknolojisi ile uygulamaların deploy edilmesi çok daha kolay ve VM’e göre çok çok hızlıdır. Continuous Integration gibi yazılım geliştirme süreçlerinde geliştiricilerin otomasyona bağladığı derleme ve test süreci sonrasında yayın süreci gelmektedir, yayın(deployment) sürecinin sorunsuz gerçekleşmesi çok önemlidir. Üretilen ve test edilen bir yazılımın kullanıcının deneyimine sunulma aşamasında kullanıcının işlerini kesintiye uğratmadan deployment tamamlanmalı ve bu işlemler hatasız gerçekleşmelidir. Container’lar bu alanda da önemli kolaylık getirmiştir ve kullanımları yaygınlaşmaktadır.

Bu konuyla ilgili daha detay için : [](https://www.docker.com/what-docker#/overview)


## Docker


Docker, yukarıda anlattığım container paltformu geliştiricisi bir firmadır. Docker’ın sunduğu yazılım araçları ile bir container tasarımlayıp bunu yayınlayabilirsiniz veya hazır container’ları kullanabilir ve bunda geliştirmeler yapabilirsiniz.

### Docker Kitematic Kurulumu


Docker denemelerinizi yapmanın en kolay yolu yine Docker’ın açık kaynaklı projesi kitematic uygulamasıdır. Bu uygulama ile görsel arabirim kullanarak ve herhangi bir komut yazma gereği olmadan Docker engine kurabilir ve container indirip kullanabilirsiniz. Uygulamanın sitesinden Docker Toolbox indirerek işleme başlıyoruz.

Kitematic sitesi : [](https://kitematic.com/)

![image](https://3.bp.blogspot.com/-rf9t0pMDjXo/WdzjPhwu3iI/AAAAAAAAAZ4/sKRrkV79o34yYxn1d2AhHnshCouVFxXowCK4BGAYYCw/s1600/1.jpg)



Kurulum işlemine devam edip gereken seçenekleri seçiyoruz.


![image](https://1.bp.blogspot.com/-Z8fFevYp3j4/WdzjU6FnljI/AAAAAAAAAaA/VUE5SwFBYGIMIn_xayNINrd6rawmpfKiQCK4BGAYYCw/s1600/2.jpg)


Kurulum tamamlandıktan sonra uygulamanın kısayollları oluşur.


![image](https://1.bp.blogspot.com/-MHUSflZKaGk/WdzjX4abp0I/AAAAAAAAAaI/h3VAkG3pescQjnhHahPBcXSWTeSPF0PKgCK4BGAYYCw/s1600/3.jpg)



Docker Quickstart Terminal’i başlatıyoruz ve gereken ayarlamaları uygulama yapıyor. Aşağıdaki gibi bir uyarı alındığında


![image](https://2.bp.blogspot.com/-o3ZsMST3fVM/Wdzjb7wQgmI/AAAAAAAAAaQ/U9HnJ8C-htYnwS36AjHshu-xwP4SxeVXACK4BGAYYCw/s1600/4.jpg)



Bilgisayarınızın BIOS ayarlarından VT-X/AMD-v tanımlarını aktif yapmanız gerekir.
Bununla ilgili bir yazı:

[](https://blogs.technet.microsoft.com/canitpro/2015/09/08/step-by-step-enabling-hyper-v-for-use-on-windows-10/)


Devamında işlemler tamamlandıktan sonra Kitematic uygulamasını açıyoruz ve docker hesabımızla giriş yapıyoruz.


![image](https://4.bp.blogspot.com/-0fniXhZNHJI/Wdzjjolf2aI/AAAAAAAAAaY/NgXMa_9DHlQx1AQ0ugUmOteqnFuG6jYrwCK4BGAYYCw/s1600/6.jpg)



İşin büyük bölümü bitti. Bu ekrana ulaştıysanız artık sadece bir container beğenip bunu indirip denemelerinizi yapabilirsiniz. Ekrandaki container listesinden bir container arayıp bulduktan sonra CREATE yaparak container’ın indirilmesini başlatıyoruz.


![image](https://1.bp.blogspot.com/-tZoQY8YIF9w/WdzjmlSMqpI/AAAAAAAAAag/JZ2iXSUQZiY3vQgRJoOeFeKUXSCNRRnWACK4BGAYYCw/s1600/7.jpg)



İndirme işlemi tamamlandığında container kuruluyor ve işlem tamamlandı.


![image](https://3.bp.blogspot.com/-JxFV9PxQ0-s/WdzjpAekyoI/AAAAAAAAAao/o8-IrWxWBk0WNW_miuGq3bsRRrmmthY-QCK4BGAYYCw/s1600/8.jpg)



Ekrandan görüldüğü üzere nginx container’ımız kuruldu ve kullanıma hazır. Settings kısmından ayarlar ve detaylı tanımlara ulaşabilirsiniz. Ayrıca Hostname/ports sekmesi altında erişim bilgilerini de görebilirsiniz. Home sayfasındaki Web Preview veya Volumes alanlarına tıkladığınızda da publish edilmiş web sayfası veya bağlanmış klasör açılacaktır.

Şimdi de MongoDB container kurup çalıştıralım.


### MongoDB Container Kurulumu ve DocumentDB Üzerinde Veri Oluşturma


Kitematic uygulamasından New ile yeni bir container arama sayfası açarak mongo kelimesi ile arama yapıp ilk gelen ve official olan mongo container Create edilir.


![image](https://2.bp.blogspot.com/-3lyXF6ZPRRc/WdzjusBhdUI/AAAAAAAAAaw/s_w_i46dj0wPpmiD5bk59JXoGuwawPXewCK4BGAYYCw/s1600/9.jpg)



İndirme ve oluşturma işlemi tamamlandığında container üzerine tıklandığında aşağıdaki gibi bir ekran gelecektir.


![image](https://3.bp.blogspot.com/-MJZINV3rZTA/Wdzjy4yFyxI/AAAAAAAAAa4/aLkB8b-9fSIg_zLnRT6kvFqn18kYOWk5wCK4BGAYYCw/s1600/10.jpg)



Böylece mongodb documentdb container’ımız kullanıma hazır. Devamında çalışan mongodb veritabanımıza veri eklemek ve incelemek isteyeceğiz.
Bunun en kolay yolu MongoDB Compass uygulaması ile yapmak olacaktır.

Uygulamanın adresi : [](https://www.mongodb.com/products/compass)

MongoDB Compass uygulamasını indirip açılışta bize sorulan IP adresi ve Port bilgilerini container’ımızdaki değerler olarak giriyoruz. Bu örnekte IP adresi 192.168.99.100 ve port 32769 olarak geçmekte yani bu değerler MongoDB Compass login ekranına girilir.


![image](https://1.bp.blogspot.com/-xvQYi6VEoM0/Wdzj1xSPohI/AAAAAAAAAbA/YJm_T2rBeEYGzrHYD8_htvuzm2TqNTdngCK4BGAYYCw/s1600/11.jpg)



Login edildikten sonra veritabanımıza erişip yeni database, collection ve document oluşturup kaydediyoruz ve bu şekilde mongodb veritabanını kullanabilir noktaya geliyoruz.


![image](https://4.bp.blogspot.com/-3vfbgFHdlhs/Wdzj44KyGfI/AAAAAAAAAbI/FNO7w-c7Y6AUPDqNdLRZmMcw_9MPW5CmwCK4BGAYYCw/s1600/12.jpg)



Yukarıdaki örnekte euldb veritabanı altındaki eulcol collection yapısı içindeki documentdb veri setindeki veriler görülüyor.
Bu noktaya gelene kadar gayet kolay araçlar ile hiç komut satırı veya kodlama kullanmadan bir container kurulumu gerçekleştirdik ve bu container’ı çalıştırıp veri alışverişi yaptık. Umarım faydalı olmuştur.

Bu container’a C# ile erişen ve veri alıp atan bir kod örneğini github repository olarak yayınladım meraklı arkadaşlar inceleyebilirler.


Github repository : [](https://github.com/enginunal/MongoDBSimpleSample)



İyi günler.
