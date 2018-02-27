
[Ana Sayfa](https://enginunal.github.io/)

# Ethereum Blockchain ve Smart Contracts Giriş


Önceki yazımı okumadıysanız ve blockchain konusunda bilgi sahibi değilseniz öncelikle (o yazıdan)[https://enginunal.github.io/BitcoinAndBlockchain] başlamanızı öneririm.  

Bu yazı, ethereum blockchain ve smart contracts konusu ile ilgili yazmayı düşündüğüm yazı serisinin ilk yazısı olmakla birlikte devamını vakit buldukça paylaşmaya çalışacağım. İlk yazıda sistemin genel hatlarını, ikincisinde kişisel bir ethereum blockchain yapılışını ve üçüncüsünde ise solidity ile smart contract geliştirip test blockchain’imize yüklemeyi gerçekleştirmeyi planlıyorum. Öncelikle ethereum’un mucidi Vitalik Buterin ile başlayalım.  


Vitalik Buterin 1994 Rusya doğumlu ve 6 yaşında Kanada’ya yerleşmiş. Kanada Toronto’da yazılımcı olarak çalışırken Bitcoin teknolojisiyle ilgilenmeye başlıyor. Bitcoin Magazine isimli web sitesinin kurucularından ve bu sitede bir çok yazı (burada)[https://bitcoinmagazine.com/authors/vitalik-buterin] yayınlıyor. 2012 yılında Waterloo Üniversitesine giriyor ve ardından 2013 yılında yayınladığı teknik dökümanla (burada)[https://github.com/ethereum/wiki/wiki/White-Paper] Ethereum isminde alternatif bir platform fikrini duyurdu. Ocak 2014'te Ethereum, Vitalik tarafından Miami'deki Kuzey Amerika Bitcoin Konferansı'nda resmi olarak ilan edildi. Ethereum kurucu ortaklarından Dr. Gavin Wood ile çalışmaya başlamasının ardından Nisan 2014’te Gavin tarafından Ethereum konulu bir teknik makale yayınlandı (burada)[https://ethereum.github.io/yellowpaper/paper.pdf].  

Devam eden süreçte Ethereum yaygınlaşmaya devam etti. Bitcoin gibi bir kripto para mimarisi sunmakla birlikte getirdiği farklılıklar nedeniyle Blockchain dünyasında yeni gelişmelere ve ilerlemelere pencere açmış oldu. Önceki yazımda Bitcoin özelinde Blockchain mimarisine değinmiştim. Kısa bir özetini vermek gerekirse, Blockchain temel olarak bir veritabanıdır. Bir veritabanının görevi olan verilerin tutulması işlemini gerçekleştirir fakat yapısal olarak farklı bir mimariye sahiptir.   

Blockchain adı üstüne birbirine bağlı bloklardan oluşmakta ve bu bloklar ise veriyi barındırmaktadır. Her blok barındırdığı veri ile birlikte paketlenir ve kriptografik olarak değişmezliği sağlanır. Blokların içindeki verinin değişmezliği kriptografik hash algoritmaları ile sağlanmaktadır. Her blok kendisinden önce gelen bloğun hash bilgisini saklar ve bu şekilde blokların geriye olarak birbirine zincir mimarisinde bağlantıları gerçekleştirilmiş olur. Verinin bloklarda depolandığı ve blokların birbirine bağlanmış olduğu ve blokların değişmezliğinin sağlandığı bu mimarinin en önemli özelliği ise dağıtık yapıda olmasıdır. Biraz önce tarif ettiğim veritabanı yapısının dağıtık olarak her bilgisayarda tutulması ve böylece veritabanı içeriğinin bütünlüğü konusunda bir konsessüs sağlanması Blockchain mimarisini oluşturur. Buna dağıtık defter de denilebilir(Distributed Ledger).   

Bitcoin ile hayatımıza giren bu yapı, varlık(asset) transferlerinde banka, aracı kurum vs(middleman) gibi bir katmana gerek duyulmadan doğrudan göndericiden alıcıya transferi mümkün kılmasıyla dikkatleri üzerine çekmişti. Ethereum ile birlikte varlık transferi özelliğinin yanında bunun programlanabilir olarak yapılması imkanı da eklemiş oldu. Ethereum dünyasında blockchain üzerinde programcıkların çalıştırılabilmesi işlemine smart contract denmekte. Smart contract konusu bu yazının ilerleyen bölümlerinde ele alınacaktır.  

Blockchain, herkese açık(public blockchain) ve sadece izinli hesaplara açık(private blockchain) olarak iki farklı türe ayrılmaktadır. Ethereum aynı Bitcoin gibi herkese açık bir blockchain mimarisi sunmakta, isteyen herkes ethereum blockchain verisine ulaşıp indirebilir, sağladığı özellikler kullanabilir, transfer işlemi, smart contract işlemleri, mining vs. yapabilir.   

Ethereum blok mimarisi olarak Bitcoin ile benzer yapıdadır ve transaction işlemleri aynı mantıkla blok içinde tutulmaktadır. Önceki yazımda blok içinde transaction’ların nasıl tutulduğu ve transaction’ların hash’lerinin alınarak bir merkle tree yapısının oluşturulması ile ilgili bazı detaylar vermiştim. Aynı şekilde ethereum da benzer yolu kullanmaktadır. Bitcoin kripto para transfer işleminde transferi yapan hesap bu işlemin girdi kısmında dijital olarak işlemi imzalar ve bu şekilde hem transfer işlemi veri bütünlüğü sağlanmış olur hem de göndericinin imzası taklit edilemeyeceğinden gönderici doğrulaması sağlanmış olur. Ethereum'da da transaction private key ile imzalanır yani  mantık aynıdır. 
Madencilik ile ilgili ise ethereum yine bitcoin’de olduğu gibi PoW(Proof of Work) algoritmasını kullanarak madenciliğin gerçekleşmesini sağlar. Aradaki fark ethereum ethash isminde bir hash algoritmasını (sha3) kullanmaktadır.   

Buraya kadar anlattıklarıma bakılırsa blockchain mimarisi, kripto para transferi ve madencilik gibi konularda Bitcoin’in getirdiklerini kullanan bir yapı ile karşılaşıyoruz. Buraya kadar olan noktada arada bir yenilik yok hemen hemen aynı mantıkla çalışıyor. Peki ethereum’un getirdikleri nedir? Neden bu kadar popüler oldu?   

Ethereum’un farkı programlanabilir blockchain olmasından kaynaklanmakta. Yani ethereum çıkana kadar blockchain yapıları üzerinde sadece kripto para transferi mümkün iken ethereum ile birlikte kullanıcılar kripto para transferi yapabilmenin yanında blockchain üzerinde program çalıştırabilecekleri bir yapıya sahip oldu.  

Ethereum, yazılan bir programın dağıtık olarak çalıştırılabileceği bir platform olarak Bitcoin’in koyduğu çıtayı bir ileri seviyeye taşıdı.  

Yazılan programların dağıtık olarak çalıştırılabilmesi konusu üzerinde durulması gereken bir konudur. Yaptığım tanımdan yola çıkarak ilk bakışta programların bir çok bilgisayarda çalıştırılması nedeniyle yüksek işlem gücü sağlanması ve paralel işlem gücü elde etmek gibi avantjların sağlandığı gibi bir durum algılansa da aslında elde edilen fayda bu değildir. Hatta Ethereum blockchain üzerinde dağıtık olarak program çalıştırmak normal bir bilgisayar üzerinde çalıştırmaktan çok daha verimsiz olacaktır.  

Çünkü bu yapı paralel programlama veya grid computing gibi mantıklar üzerine kurgulanmadığından veya amacı bu olmadığı için yüksek işlem gücü veya performans elde etmek mümkün değildir. Buradaki asıl amaç çalıştırılan programın hiç bir zaman çökmemesinin garanti edilmesi, programa müdahalenin mümkün olmaması, hata toleransının sağlanması, programa sağlanan verinin blockchain üzerinden alınması nedeniyle değiştirilemez veri garantisinin verilmesidir. Yukarıdaki nedenlerle blockchain üzerinde çalıştırılacak programın geliştirilmesi sürecinde ethereum'un yetenekleri ve sundukları iyi anlaşılarak planlama yapılması projenin başarısı için kritik önemdedir.  

Performans ve paralel programlama gibi faydaları yoksa programlanabilir blockchain mimarisi bize ne gibi yenilikler getiriyor?
Diyelim ki bir program yazmak ve bunu ethereum üzerinde yayınlamak istiyoruz. Ne gibi programlar yazabiliriz bu sorunun cevabı yukarıdaki sorunun da cevabı olacaktır.   
Örneğin tapu işlemlerini bu yapı ile gerçekleştirmek mümkün, bir eviniz var ve ethereum üzerinden satış işlemi yapacaksınız alıcı parayı gönderdi ve eve ait dijital satış işlemini onaylayacak rutinleri otomatik başlatacak program geliştirebilirsiniz. Örnekleri çoğaltırsak oy verme işlemleri, kontratlı satışlar, ev veya aracınızın sigorta işlemlerinin otomatik olarak gerçekleştirilmesi, sağlık sektörü hasta kaydı işlemleri, IOT ve akıllı cihazlardan verilerin alınıp işlenmesi vb. bir çok alanda bu mimari kullanılabilir.  

Görüldüğü gibi bu sistemin kullanım alanı yazdığınız program ve hayal gücünüz ile oldukça genişleyebilecek bir yelpazeye sahip. İşte bu nedenle çok farklı sektör ve alanlarda karşımıza çıkacak bir mimari tanımını yapmak yanlış olmaz. Teknik olarak en basit anlatımla çalışacak programın yaptığı işi şu şekilde tanımlayabilirim : IFTT (IF THIS THAN THAT) yani
Bir işlem gerekli kuralı sağladığında diğer işlemin gerçekleştirilmesi.  

Buraya kadar kavramlarda fazla kaybolmadan anlaşılabilirliği sağlamaya çalıştım, Umarım konuyu bilmeyen için biraz daha netleşmiştir. Şimdi bazı kavram ve özelliklere bakalım.  


## Hesaplar  

Ethereum hesap tipleri ikiye ayrılmaktadır.  

* Externally Owned Accounts (EOA)   
* Contract Accounts  


EOA, private key tarafından kontrol edilir. Bitcoin’de olduğu gibi genel kullanımdaki normal hesaplardır. Bir hesap için private key sahibi iseniz o hesaptaki ether transferi dahil tüm transaction işlemlerini gerçekleştirme yetkisine sahipsiniz demektir. Sahip olduğunuz ether miktarını tutar ve transfer işlemleri yapmanıza imkan tanır.  

Contract Accounts, yönetiminin kodlanmış program tarafından yapıldığı hesaplardır. Sahip olduğu ether miktarını tutar. Bu hesap tipinde programın çalışması diğer hesaplardan gelen transaction veya message ile tetiklenir.  

Hesaplar konusu contract konusunu da içerdiğinden burada sonlandırıp smart contract bölümüne geçelim.  



## EVM ve Smart Contract  

EVM, Ethereum Virtual Machine kelimelerinin kısaltması olmakla birlikte blockchain üzerine gönderilen programların çalıştırılmasını üstlenen altyapıdır. Önceki konuda, geliştirdiğimiz programların dağıtık yapıdaki bilgisayarlara gönderilip çalıştırıldığından bahsetmiştim, çalıştırma işlemi EVM tarafından yapılır. Yazılan programa ise Smart Contract (Akıllı Sözleşme) olarak adlandırılır. Genelde akıllarda Smart Contract kavramı ile ilgili yanlış algılar oluşmasına neden olan şey ise isimlendirilmesi. İçinde kontrat kelimesi geçse de bizim anladığımız anlamda bir kontrat değildir. Aslında temel olarak bilinmesi gereken tanım, ethereum’a bağlı bilgisayarlarda mining işlemi sırasında çalışan programlardır. Bu programların hangi yeteneklere sahip olabileceği tamamen geliştiricilerin hayal güçleri ile ilgilidir. İstenirse karşılıklı bir sözleşme olarak ta geliştirilip yayınlanabilir veya istenirse hava durumu bilgisini otomatik olarak IOT cihazından alıp kaydeden bir program olarak ta yayınlanabilir.  

Örneğin Ali ve Ayşe aralarında bir iddiaya girdiler. Ayşe’nin iddiasına göre iki gün sonra dolar 4TL ve üzeri olacak. Ali’ye göre bu mümkün değil. Kaybedenin 100TL’yi kazanana vereceği konusunda aralarında anlaştılar. Fakat ikisi de birbirine para işlerinde hiç güvenmiyor, bunu smart contract kullanarak çözebileceklerini bilerek bir smart contract geliştirdiler.  
Buna göre smart contract’ın yaptığı iş şu şekilde olmaktadır:  
Smart contract Ali ve Ayşe’den 100’er lira alarak süreci başlatır ve iki gün sonra merkez bankası kur sisteminden güncel kuru çekerek kimin kazandığına karar verir ve 200TL’yi kazanan kişiye transfer eder.   

Smart contract’lar ethereum ağındaki diğer kullanıcılar gibi kripto para alıp gönderim yapabilir, diğer smart contract’lara mesaj gönderebilir. Onları tetikleyebilir. Bu şekilde birbirinin devamında farklı süreçleri işleten bir smart contract zincir süreçleri geliştirilmesi de mümkündür.  

Smart contract geliştirme süreci Solidity programlama dili ile yapılmakta. Solidty, C++ ve Java dillerinin yazım yapısına benzeyen bir programlama dilidir. Solidity ile smart contract yazılım süreci gerçekleştirildikten sonra Solidity derleyebilen bir derleyici ile derlenir ve blockchain’e transaction olarak iletilir.   

  
Örnek bir smart contract kodu:  

```
pragma solidity ^0.4.0;

contract SimpleStorage {
    uint storedData;

    function set(uint x) public {
        storedData = x;
    }

    function get() public constant returns (uint) {
        return storedData;
    }
}
```
  

Browser tabanlı ve offline olarak Solidity kodlarını derleyip test edebileceğiniz derleyici olarak (https://github.com/ethereum/browser-solidity/tree/gh-pages)[https://github.com/ethereum/browser-solidity/tree/gh-pages] adresindeki zip dosyasını indirip deneyebilirsiniz.  
Solidity ile ilgili daha detaylı bilgi ve uygulama örneğini sonraki yazılarımda eklemeyi planlıyorum o nedenle programlama kısmını kısa tuttum.  


Smart contract’ların ve diğer transaction işlemlerinin gerçekleştirilebilmesi için bir ücretlendirme sistemi mevcuttur. Bunun için gas adı verilen birim kullanılır.Transaction işlemi veya Smart contact kodunun çalışabilmesi için gerekli gas miktarı ve kullanabileceği maksimum gas miktarı belirlenir. Aslında bu yapıyı Bitcoin’deki transaction fee yani işlem ücretine de benzetebiliriz. Smart contract için ise kullanılan işlem gücü, veri erişimi,, kullandığı kaynak veya diğer belirleyici unsurlara göre çalışması için gereken gas miktarı artacaktır.Smart contract çalıştırmak için gereken gas harcamaları, hesabınızda bulunan ether ile satın alınır. Programı çalıştırmak için gaz gereksinimlerini karşılayacak yeterli ether yoksa, işlem iptal olur ve tüm ara durum değişiklikleri işlem öncesi anlık durumuna geri döner.  

Gas, Ethereum'daki karmaşık hesaplamaları ağ üzerinde çalışmak için "güvenli" hale getiren kilit mekanizmadır, çünkü kontrolden çıkmış programlar yalnızca çalıştırılmasını isteyen insanlar tarafından sağlanan para kadar sürecektir. Para durduğunda, madenciler bu işlem üzerinde çalışmayı durdururlar. Bu şekilde ücretsiz program çalıştırma olanağı olmayacağından sisteme olan DDOS gibi olası saldırıların maliyeti yüksek olacaktır ve bir anlamda sistem güvenliği için koruyucu bir mekanizma sayılabilir.  


Yazıda konuların uzamasından dolayı değinemediğim bazı noktalar olmakta kafa karışıklığı yaratmamak adına burada bitiriyorum. Umarım faydalı olmuştur. Devamındaki yazılarda görüşmek üzere.  
  
  
  
Engin ÜNAL

