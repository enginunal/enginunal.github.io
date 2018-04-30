[Ana Sayfa](https://enginunal.github.io/)

# Bitcoin ve Blockchain Nedir? Nasıl Çalışır?

Son yıllarda yükselen değerleriyle ve spekülasyonlarıyla dikkatleri çeken kripto paralar ve bu paraların başlangıç noktası olan Bitcoin nasıl bir mimariye sahip, güvenliği nasıl sağlanıyor ve teknik olarak hangi farklılıklar getirdi. Bu yazıda Bitcoin özelinde Blockchain teknolojisi ve çalışma presipleri incelenecektir.  
Hızla okunabilecek ve kolay anlaşılabilir bir yazı olması dileğiyle konuya başlayalım.  
Bitcoin, 2008 yılında Satoshi Nakamoto isminde birinin ilk teknik dokümanı paylaşmasıyla ([https://bitcoin.org/bitcoin.pdf](https://bitcoin.org/bitcoin.pdf) ) gün yüzüne çıktı ve 2009 yılında aktif olarak kullanıma açıldı. Nakamoto, Bitcoin ismini ve teknik detayını açıkladıktan ve sistemin stabil hale gelip çarkların dönmesini sağladıktan sonra kayıplara karıştı ve arkasında bir çok soru işareti ve spekülasyon bıraktı. Aslında bu ismin bir takma ad olabileceği veya bir gruba ait olabileceği veya bunun derin bazı yapıların başlattığı bir proje olduğu gibi pek çok spekülasyon hala yapılıyor.  
Sonuçta böyle birisi var mı veya Bitcoin fikri nasıl bir süreçle ortaya atıldı ve kimler devredeydi bilinmiyor, en azından biz bilmiyoruz. 
Fakat şunu biliyoruz ki bu mimari ortaya atıldığından bu yana dünyada kendisine çok önemli bir yer edindi ve yolundan giden onlarca farklı alanda farklı teknolojiler de bulunmakta. Peki o kadar etki bırakmasının nedeni sadece sanal bir para olması mıdır? Bu soruya yanıt tabiki hayır olacaktır.  

Bitcoin, Blockchain kullanması ve bu veri yapısının merkezi bir yerde tutulması yerine dağıtık(decentralized) olarak tutulması bunu da uçtan uca(P2P) ağ yapıları kullanarak sağlaması gibi daha önce zaten var olan fakat bir araya gelmemiş konseptleri bir araya getirerek bunların ortak çalışmalarını sağlayan bir mimari örneğinin başarısını gösterdi.  

Bunun yanında para transferlerinin göndericiden alıcıya doğrudan ve aracı kullanılmadan iletilmesini sağladı. Para gönderen ve alanın kimlik veya diğer kişisel tanımlayıcı detayları içermemesi sayesinde kullanan kişinin kim olduğunun sistem de dahil kimse tarafından bilinmemesi gizliliğini sağladı. Bunun yanında P2P yapı üzerinden yapılan işlemlerin tüm bağlı uçlara(Node) bildirilmesi nedeniyle tüm uçların sürekli tüm işlemleri kaydetmesi ve üzerinde konsensüs oluşan ve dijital imzalı olarak paketlenmiş işlemlerin deftere eklenmesi ve her uçta bu defterin bir kopyasının bulunması kayıt güvenliğini getirmiştir.  

Bu gibi özellikler detaya inilerek artırılabilir. Adım adım gidersek Bitcoin ve tüm kripto paraların Blockchain veri yapısı üzerinde çalıştığından bahsetmiştim. Öncelikle ilk konu başlığı bence Bitcoin’in yazılım dünyasına getirdiği ve çok farklı alanlarda da uygulamaları bulunan Blockchain nedir ona bakalım.  


## Blockchain  

Blockchain en temel olarak bir veritabanının üzerinde çalışan protokoldür ve birbirine doğrudan bağlı bilgisayarlar(P2P ağı) aracılığı ile bu veritabanının kopyası tutulmaktadır. Yani bir merkez veya sunucu yoktur. Tüm bağlı bilgisayarlar sürekli olarak veritabanının güncel kopyasını kendisinde tutar. Yani ağa bağlı her bilgisayar başlangıçtan itibaren tüm işlemleri içeren tam kopyayı saklar.
Aslında blok zinciri konusunda buraya yaptığım tarif dağıtılmış defter teknolojisi ile aynıdır. Dağıtılmış Defter Teknolojisi (Distributed Ledger Technologies) veya DLT mimarisinde de defter kayıtları dağıtılmış yapıda tutulmaktadır. Bitcoin de Blockchain defterinde işlemleri bloklar halinde ve dağıtılmış bilgisayarlarda açık olarak tutmaktadır. Fakat bundan sonraki anlatımlar DLT ile Blockchain’in farkını ortaya koymaktadır.  

Bu veritabanı nasıl bir yapıdadır? Veriler nasıl tutulur?  

Blockchain adı üstünde blok-zinciri, birbirine bağlanmış bloklardan oluşmaktadır. Tüm veriler bu bloklar içinde tutulmaktadır. Burada kolay anlaşılması açısından blokları tablo gibi de düşünebiliriz. Bloklar belli sayılarda işlemi barındırırlar ve her blok kendisinden önceki bloğa bağlanarak blok zincirine eklenmiş olur. Zincirin başlangıcı olan bloğa genesis block ismi verilir. İlk blok herhangi bir bloğa bağlı değildir.  

Blokların bağlantıları bilgisayar yazılım eğitimlerinde anlatılan veri yapıları konu başlığındaki bağlı liste(linked list) veri yapısına benzer tek farkı tersine bağlıdır(back-linked list). Yani bir blok kendisinden önce gelen bloğun adresini kendi içinde saklar. 
Tanımı biraz daha özelleştirirsek Blockchain birbirine kronolojik olarak bağlı ve tüm işlemlerin tutulduğu yapılar olan bloklardan oluşur. Bu bloklar madenciler(miner) tarafından bir dizi kriptografik ve matematiksel işlemle onaylanır, paketlenir ve zincire eklenir.   

Blockchain veri yapılarının uçtan uca birbirine bağlı bilgisayarlar ile ağ mimarisinde güncel olarak tutulduğundan bahsetmiştim, bu sayede blok zincirinin tek merkezde tutulmasına kıyasla daha iyi korunacağı açıktır. Dünyanın bir bölgesindeki bilgisayarların aynı anda çökmesi söz konusu olsa bile bu yapı nedeniyle sağ kalan bilgisayarlar işlemlerin devam etmesini sağlayacaklardır.  

![image](/images/BitcoinVeBlockchain/1.png)  

Blockchain’deki blokların her birinin bir öncekine referans etmesi nedeniyle örneğin zincirdeki blokların arasına kaçak bir blok eklenmek istendiğinde eklenen bloğun kendisinden sonra gelen tüm blokları etkilemesi ve bu şekilde zincire olabilecek müdahalelerin engellenmesi sağlanmıştır. Bu mekanizma nasıl işliyor kısaca ona bakalım. Her blok bir önceki blok özetinin hash değerini kendi içinde tutmakta. Ve her blok aynı zamanda kendi hash bilgisini de bulundurmakta. Bu şekilde bloğumuzun değiştirilemez olması sağlanırken, bloklar arasındaki bağlantıların da değiştirilemez olmasını sağlamakta. Hash’lenmiş bir veride en ufak bir değişiklik hash’in tamamen değişmesine yol açmaktadır.  

Hash Nedir?  
Bitcoin SHA-256 olarak bilinen 256-bitlik Kriptografik Hash kullanmaktadır. Kriptografik hash metodu kendisine verilen bir veriyi çözülemez ve tahmin edilemez şekilde şifreler. Hash kelimesini temel olarak şifreleme veya karıştırma olarak anlayabiliriz. Bir mesajın hash’lenmesi onun şifrelenmesi olarak düşünülebilir.  
Bir mesajı veya bir veriyi hash fonksiyonundan geçirdiğimizde yani hash işlemini uyguladığımızda sonuç olarak şifreli bir veriye sahip oluruz ve bu sonuç değeri kullanılarak mesaja ulaşmak mümkün değildir. Mesajda bir karakter bile değişse hash tamamen değişmektedir. Bu nedenle çok uzun iki mesajı karşılaştırmak için hash’lerini karşılaştırmak iyi bir yöntemdir.  
Bir mesajın hash değeri her zaman aynıdır. Yani mesaj her hash’lendiğinde aynı sonucu döndürür.Kısacası hash değeri elimizdeki mesajın bütünlüğünün kanıtıdır.  

Hash konusunu hızlıca açıkladıktan sonra bu hash değeri alınmış ve değişmezliği sağlanmış bloklardan oluşan zinciri bozmak mümkün değil mi?   
Öyle olsaydı zaten bu yapı bugünleri göremezdi. Bu nedenle bu sorunun cevabı açıktır. Fakat açıklanması anlaşılması anlamında önemlidir. Blok üretmek madencilerin yüksek işlem gücü kullanarak gerçekleştirdiği süreçlerdir.  

Blok, bir dizi matematiksel işlem ve hash işlemi gerektiren ve adına Proof of Work denilen süreç ile üretilir. Blok üretiminin ortalama on dakika sürmesi planlandığından işlem gücü artsa da zorluk derecesi artırılarak üretim zorluğu da artar. Bu sayede işlem gücü ne kadar artarsa artsın blok üretimi belli bir periyotla devam eder. Bu da blokların daha yüksek işlem gücü gerektiren işlemlerden geçmesine neden olarak güvenliği artırır. Proof Of Work konusu daha sonra incelenecektir.  

Görüldüğü üzere blok üretmek yüksek işlem gücü ve zaman gerektiriyor. Peki blok içindeki işlemler ne kadar güvenli?  
Diyelim ki bir atak planladık bu atak senaryosunda biz Ahmet’e para gönderme işlemi gerçekleştireceğiz aynı parayı Ali’ye de göndereceğiz. Kısacası paramızı hem Ahmet hem de Ali’ye aynı anda göndermeyi deneyeceğiz. Ahmet ve Ali den hangisine para ulaşır ikisine de gider mi? Bu tip ataklara double-spend attack denmektedir. Yani aynı harcamanın iki kez yapılması. Her iki işlem kaydı(transaction) Bitcoin doğrulanmamış işlem havuzuna(unconfirmed pool) girmektedir. Ancak sadece ilk işlem kaydımız onaylanır ve bir sonraki blokta madenciler tarafından doğrulanmış olarak eklenir.  
Bunun nedeni blok üretimi gerçekleşirken her işlem kaydının dayandığı önceki işlem kayıtları da taranır ve harcanan para daha önceden harcanmışsa bunu madenciler geçersiz saydığından ikinci işleminiz yeterince onay alamaz, bu nedenle de Bitcoin ağıdan düşürülür.   

Ya işlemler madenciler tarafından eşzamanlı olarak işleme alınırsa? Madenciler işlemleri aynı anda havuzdan çektiğinde ve blok içinde aynı anda yayınladığında, bu bloklar önceki bloğa çatallanarak bağlanmış olur. Çatalda en uzun devam eden blok kalır diğer dal silinir. Bu oldukça karışık oldu işlemi biraz daha açık hale getirmeye çalışayım.  

Bir madenci A bloğunu hazırladı aynı anda diğer madenci B bloğunu hazırladı, aynı bloğu referans eden iki blok oluştu. Madenciler blokları aynı anda hazırladığı için hangisi ile yola devam edilecek karar verilmesi gerekiyor. O anda zincirin en son bloğu X olsun. X bloğuna A ve B bloğunun ikisi de bağlanır. Bu durumda zincir de bir çatal (fork) oluştu. Hem bizim hem dünyadaki diğer tüm madencilerin blok üretme yarışı çatalın çözülmesi sağlanana kadar devam edecektir. A bloğuna bağlanan ve devam eden zincir, B bloğuna bağlanan ve devam eden zincirden daha uzun ise A bloğu ile yola devam edilir ve B bloğu zincirden çıkarılarak çatal düzeltilir.  

Böyle bir atağın daha önce başarılı olamamasının nedeni tek başımıza erişmemiz mümkün olmayan oldukça yüksek bir işlem gücü gerektirmesidir. Yani sahte işlemler içeren bir bloğun zincire eklenmesi ile iş bitmemekte o bloğun desteklenmesi yani devamındaki blokların da üretilmesi gerekmektedir. Bu da tüm dünyadaki madencilerin kullandığı işlem gücünün yarısından fazlasına sahip olmanız anlamına gelir, bu da yetmez arka arkaya herkesten önce yeni blokları siz eklemeye devam etmelisiniz, blok üretmek için kullanılan algoritmanın işlem gücü ve şans faktörüyle çalıştığı dikkate alınırsa buna ulaşmak pek mümkün görülmemektedir.   

Genel olarak yaptığınız bir işlemin çeşitli ataklara karşı güvenli olması altı blok sonrasını görmesi olarak kabul edilmektedir. Yani sizin transfer işlemleriniz 1 nolu blokta olsun. Bu bloktan sonra gelen bloklardan 7 nolu blok üretildiğinde ve zincire eklendiğinde sizin işlemleriniz de güvende ve değişmez olarak görülebilir. Bu Bitcoin için genel kabul gören bir yaklaşımdır. İşlemlerinizi içeren blok ne kadar eskide kalırsa işlem kanıtınız o kadar kesinleşir. Bu kabul şimdiye kadar olan çatallanma ve onay istatistiklerine göre çıkarılmış genel bir yaklaşımdır.  

## Blok

Blok, Blockchain mimarisinde zinciri oluşturan yapılardır. Bloklar birbirine bağlıdır ve her yeni gelen blok zincire kendisinden öncekine bağlanarak dahil olur. Bloklar, tüm işlemleri içeren ve işlemlerin güvenliğini sağlayan yapılardır. Bu nedenle kendi içerilerinde tüm bu güvenliği sağlayan kontol alanları bulunmaktadır.  

Peki blok içinde neler var? Bir Blok, o bloğu tanımlayan ve özetini içeren bir blok başlığı(Block Header) ve işlem kayıtlarından(Transactions) oluşur. Bitcoin için her blok içinde 500’den fazla işlem (transaction) bulunur. Ortalama olarak işlem boyutu 250 byte civarındadır. Blok başlığı ise 80 byte veri içerir.  
  
Bitcoin Blok yapısı:  

| Alan | Boyutu | Açıklaması |
| --- | --- | --- |
| Blok Büyüklüğü | 4 byte | Toplam blok büyüklüğü |
| Blok Başlığı | 80 byte | Blok başlığının büyüklüğü|
|İşlem Sayısı | 1-9 byte | Blok içindeki işlem sayısı|
|İşlemler | Değişken | Blok içindeki tüm işlemler|

Bitcoin Blok Başlığı yapısı:  

| Alan | Boyutu | Açıklaması |
| --- | --- | --- |
|Versiyon | 4 byte | Yazılımın versiyonu|
|Önceki Blok Hash | 32 byte | Referans edilen önceki bloğun Hash değeri|
|Merkle Root | 32 byte | Merkle root hash değeri|
|ZamanDamgası | 4 byte | Bloğun yaratılma zamanı|
|Zorluk Derecesi | 4 byte | Proof Of Work algoritması zorluk hedefi|
|Nonce | 4 byte | Sayaç(PoW tarafından kullanılacak)|

  
  
## Merkle Ağacı

Bitcoin blok zincirindeki her blok, bir merkle ağacı kullanarak bloğun tüm işlemlerinin bir hash’ini içerir. Merkle tree, aynı zamanda binary hash tree olarak da bilinir. Büyük veri kümelerinin bütünlüğünü verimli bir şekilde hash’lemek ve doğrulamak için kullanılan bir veri yapısıdır. Merkle ağaçları kriptografik hash’ler içeren ikili ağaçlardır. "Ağaç" veya tree terimi, dallanmış bir veri yapısını tanımlamak için bilgisayar bilimlerinde kullanılır.  

Tam olarak yapılan şudur; Blok içindeki tüm işlemler(transactions) hash’lenir elde edilen iki hashler ikişer olarak birleştirilip bir üst seviyede tekrar hash’lenir. Bu şekilde ikişer ikişer döngüsel olarak tek hash kalana kadar işlem devam eder. Kalan bu hash değerine de dijital parmak izi(Merkle Root) denir.  
Bir işlemin bir bloğa dahil olup olmadığını doğrulamak için çok verimli bir süreç sağlamaktadır. Merkle Root elde edilince bunu Blok Header’a yazar. Bitcoin'in merkle ağaçlarında kullanılan şifreleme hash algoritması, SHA256'dır.  

![image](/images/BitcoinVeBlockchain/2.png)  
  
    
      
      
## İşlemler  

Blokların işlem kayıtlarını sakladığından ve işlemlerin güvenliğinin bloklar tarafından sağlandığından bahsetmiştim. İşlem nedir? Neden bu kadar önemlidir? İşlem kaydı(transaction) en basit anlatımla para transferidir. Hesabınızdaki mevcut kripto paranın başka birine gönderilmesi bir işlem kaydı oluşturur ve bunun gibi her hareket birer işlem olarak kabul edilir. Yapılan her işlem herkese açıktır ve Blockchain defterindeki blok içinde saklanır. Aslında tüm yapı bu transfer işlemlerinin doğru ve güvenli sağlanması üzerine inşa edilmiştir. O nedenle işlemler tüm mimarinin en temel ve en önemli yapı taşıdır.  
İşlem, bir değerin(bitcoin) bir yerden(input) diğerine(output) transferini sağlayan kayıttır.  
Blok içindeki tüm işlemlerin hash değerleri alınır ve merkle tree yapısı ile bunların değişmemesi garanti altına alınmış olunur. Ayrıca bloklar da değişmezliklerini header hash‘leri ile sağlarlar. Bu şekilde hem blokların değişmezliği hem de bu blok içindeki işlemlerin değişmezliği garanti altına alınmış olur. Şimdi işlem veri yapısını inceleyip en yaygın yapılan bir işlemin nasıl gerçekleştiğinden bahsedeceğim.  

Bitcoin işlem veri yapısı Girdi verileri ve Çıktı verilerinden oluşmaktadır, bunlar işlem içinde referans edilmektedirler. Genel yapı aşağıdaki gibidir:  

| Alan | Boyutu | Açıklaması |
| --- | --- | --- |
|Versiyon | 4 byte | İşlemin hangi kurala uyacağını belirler|
|Girdi Sayısı | 1-9 byte | Girdi(input) sayısı|
|Girdiler | Değişken | İşlem girdi verileri|
|Çıktı Sayısı | 1-9 byte | Çıktı(output) sayısı|
|Çıktılar | Değişken | İşlem çıktı verileri|
|Kilit Zamanı | 4 byte | Unix zaman damgası veya blok no|

Çıktı veri yapısı:  

| Alan | Boyutu | Açıklaması |
| --- | --- | --- |
|Miktar | 8 byte | Bitcoin miktarı, (satoshis olarak, 1satosih=10-8 BTC)|
|Kilit-Script Boyut | 1-9 byte | Kilit-Script büyüklüğü|
|Kilit-Script’i | Değişken | Çıktı miktarını harcama koşullarını tanımlayan script.|


Girdi veri yapısı:  

| Alan | Boyutu | Açıklaması |
| --- | --- | --- |
|İşlem Hash Değeri | 32 byte | Harcanmamış para işlemini içeren işlem kaydına referans eden hash değeri|
|Çıktı İndeksi | 4 byte | Harcanmamış para içeren işlem kaydı içindeki indeks no|
|Kilit Açma Script Boyutu | 1-9 byte | Kilit Açma scripti büyüklüğünü belirtir|
|Kilit Açma Scripti | Değişken | Harcanmamış paranın serbestçe kullanılmasını sağlayacak script içeriği|


Konuyu açıklayabilmek için yukarıdaki veri yapılarına girip girift işlemlerin detaylarına gömülmeden bir transferin nasıl gerçekleştiğini ve işlem nedir onu anlatmaya çalışacağım.   

Her işlem en az bir girdi ve bir çıktı içerir. Her girdi, kullanacağı parayı bir önceki çıktıdan alarak harcar. Daha sonra, her çıktı, daha sonraki bir girdi bunları harcayana kadar Harcanmamış İşlem Çıktısı (UTXO - Unspent Transaction Output) üretir. Bitcoin cüzdanınız size 10 bitcoin’e sahip olduğunu söylüyorsa; bu, aslında bir veya daha fazla UTXO kaydında toplamda 10 bitcoin harcanmayı bekliyor anlamına gelir. Bitcoin para transferinde işlem içinde meblağ tutarlılığı sağlanmak zorundadır.   

Yani başka bir harcanmamış para içeren işlemden alınan paraların toplamı(input transactions), harcanan(output transactions) ile aynı veya fazla olmalı, işlem balansı her zaman sıfır veya üzeri olmalıdır. Başka bir anlatımla bir işlem kaydında başkasına transfer edilen para o kayda referans eden para kayıtlarının toplamına eşit veya ondan az olmalıdır.  

input bitcoin => output bitcoin 

Peki işlem kaydına gelen para çıkan paradan büyük oldu diyelim aradaki fark ne oluyor? Bu durumda aradaki fark miner’lara gitmek üzere transaction fee olarak adlandırılan bahşiş olmaktadır. Konunun devamında ona da değineceğim.
Eğer benim önceki işlemlerimin çıktısından toplam 10 bitcoin’im var ve ödemem gereken 5 ise kalan 5 ne olacak? 5 bitcoin bahşiş mi vereceğim? Bu durumda yukarıdaki işlem için kalan 5 bitcoin’i kendime yönlendirebilmekteyim. Bahsettiğim iş UTXO çıktısı üretilerek gerçekleşir. Yani 10 bitcoin’i önceki input transaction’dan referans ederek aldınız ve output transaction olarak Ahmet’e 5 bitcoin gönderirken yine kendinize 5 bitcoin UTXO çıktı göndererek hesabı kapatırsınız.  

Şimdi Transaction Fee denilen bahşiş çıktısını inceleyelim. Bu bahşişler Bitcoin network tarafından sistemsel olarak belirlenir ve transferi yapılan para ile miktarına göre değişmez.   

Transaction Fee’ler o transaction’ları blok içine alıp yayınlayan miner’lara verilmektedir. Bu da mining işleminin özendirici taraflarından biridir. Bir blok içinde yer alan yüzlerce transaction içindeki bahşişler miner’lara ödül olarak verilerek mining işlemine daha çok katılımın sağlanmasına yol açar ki bu da sistemin toplam işlem gücünü yani güvenliğini yükselten etki yaratır. Miner’lar sadece transaction fee almazlar, bunun yanında ürettikleri blok için coin base transaction denilen işlemle transaction listesinin başına yeni Bitcoin üretimi anlamına gelen ve kendilerine ödül olarak iletilen miktarları da alırlar. Coin base transaction bir tür para basma işlemidir ve input bilgisi yoktur sadece output bilgisi bulunmaktadır, miner’lar blok üretimini tamamladığında yeni üretilen bu transaction’ı da transaction listesine ekler ve bu transaction tarafından üretilen Bitcoin miktarına sahip olurlar.   
Bu rakam 2009 yılında blok başına 50 bitcoin iken her dört yılda yarı yarıya düşerek devam etmektedir. Bu hesaba göre 2140 yılına kadar bitcoin üretimi tamamlanacak ve yeni blok üretiminde bitcoin üretilmeyecek ve toplam bitcoin miktarı ise 21 milyon civarında olacaktır.  

Konumuz olan işlemlere tekrar dönersek, özetle işlemler yani transactions temel olarak muhasebe kayıtlarının tutulduğu yapılardır. Bitcoin’de hesap kaydı ve toplam para gibi bir yapı olmadığından bir işlemde aktaracağınız para önceki işlemden devir alınır ve bu şekilde devam eder. Her işlem kaydı kendi içerisinde dengeyi sağlamalıdır. Bir işlem kaydı içinde birden çok girdi ve birden çok çıktı olabilir. Her input işlemi daha önceki output işlemine referans vererek sürekliliği ve birbirine bağlantıyı sağlar. Eğer bitcoin cüzdanınız size 10 bitcoin’iniz olduğunu söylüyorsa aslında yaptığı iş en başa kadar gidip bu tüm işlemleri tarayarak size ait olan ve harcanabilir bitcoin içeren işlemlerdeki bitcoin miktarını topladığı ve sonucun 10 bitcoin çıktığı anlamına gelmektedir.  

Her bir işlem kaydı(transaction) bir hash'e sahiptir ve hash değeri bu işlem kaydının tanımlayıcı imzasıdır denilebilir. Aynı zamanda işlem kaydının değişmezliğini sağlar. İşlem kaydı içindeki en ufak bir değişiklik hash değerini de değiştirmektedir.  

Girdi ve çıktı işlemlerinin çalışma mantığı şu şekildedir:  
İşlem kaydı içindeki girdi yapısında harcanacak bitcoin'lerin hangi işlem kaydı çıktısından geldiği tutulur(kullanılacak transaction hash'i ve output indeksi). Bunun yanında işlem kaydı girdisi içerisinde dijital imza da bulunmaktadır. Transfer sırasından girdiler hazırlanırken dijital olarak imzalanır. Dijital imza ve güvenliği konusu başlı başına bir yazı konusu olduğundan girmeyeceğim.  

İşlem kaydı çıktısı içinde ise gönderilecek miktar ve bu miktarı kullanabilecek alıcının sağlaması gereken bazı kurallar dizisi ve alıcının adresi yazılır. Bu kurallar ödemenin kim tarafından ve nasıl kullanılacağını belirleyen kurallardır. Transaction output içinde script alanı bu işlem için kullanılmaktadır.   


  
## Proof Of Work

Önceki bölümlerde blok üretiminin madenciler tarafından gerçekleştirildiğini ve bunun matematiksel süreçlerden geçerek sağlandığını kısaca açıklamıştım. Her blok zincire eklenmeden önce bazı kriptografik işlemlerden geçer ve önceden tanımlı şartlara uyarsa zincire eklenir. Bu şartları madenciler gerçekleştirmektedir. Madencilerin blok üretiminde yaptığı işin ispatı ise matematiksel olarak sağlanmaktadır. Bu kavrama da Proof Of Work denir. Aslında Proof Of Work nedir bunu anlayabilmek için madencilik ve madencilerin ne yaptığını bilmek gerekir ve bu bilgi PoW sistemini anlamak açısından yeterlidir.   

Madencilerin görevi Bitcoin işlem havuzundaki işlemleri alıp birleştirip bunların matematiksel olarak bütünlüğünü sağladıktan sonra blok bütünlüğünü verilen kurala göre sağlamak ve yayınlamaktır. Sistem tanımı gereği zincire yeni blok ekleme süreci on dakika olarak belirlenmiştir. Artan işlemci gücü ve bütünleşik işlem gücü nedeniyle bu sürenin sabit tutulması ancak bu kuralların gittikçe zorlaştırılması ile mümkündür. Peki bu kural en kısa anlatımla nasıl işler? Blok’ların hash değerlerine sahip olduğunu bu hash değerlerinin de blokların tanımlayıcı numarası(ID) olduğundan bahsetmiştim. Blok’lar kendisinden önce gelen bloğa bu hash değerini referans göstererek bağlanırlar. Örnek olarak biraz önce üretilen bir bloktaki hash değeri:  

```
0000000000000000000344254c5d61a2da8a2317a644b7caff40fa2788c4ee72  
```

olarak belirlenmiş. Bir bloğun hash değerinin hesaplanması günümüz işlem gücünde saliseler civarında ve gözardı edilebilen hızdadır. Fakat bu hash değerinin yukarıda görüldüğü gibi 19 sıfır ile başlayanının bulunması ise oldukça yüksek işlem gücü gerektiren ve olasılık kurallarının devreye girdiği bir durumdur. Örneğin ilk bloğun hash değeri on sıfırla başlamaktaydı. Zaman içinde soldaki sıfır sayısı artmaktadır bunun nedeni ise daha yüksek işlem gücü ile blok üretimi gerçekleştiğinden on dakika kuralına göre üretimin zorlaştırılması ile açıklanabilir.   

Madenciler başta olması gereken sayıda sıfır içeren hash’ler bulmak için tüm olasılıkları deneyerek hash üretirler ve ürettikleri hash bu koşulu sağlıyorsa yayınlarlar. Bu blok zincire eklendiğinde ise blok içindeki bahşiş ve yeni üretilen bitcoin işlem kaydına da sahip olurlar. Peki blok içeriği değişmezken ve değişmeyen verilerin hash’i de değişmiyorken nasıl farklı hash değerleri ortaya çıkmakta? Bunun açıklaması nonce değeridir. Başlarda blok konusunda blok içindeki alanları listelediğim tabloda nonce alanı da bulunmakta. Her hash işleminde nonce değeri değiştirilerek farklı hash’ler üretilir. Ve uygun hash’e ulaşıldığında o nonce değeri de blok içine yazılmaktadır.  

Temel olarak madencilik işlemi bu şekilde gerçekleşmektedir. Proof Of Work, Bitcoin tarafından Blockchain’e eklenecek Blok’ların belli bir işlem gücünün ürünü olması ve bu işlem gücünün matematiksel temellerle ispat edilmesi prensibine dayanır. Blokların yüksek işlem gücü gerektiren kriptografik proseslerden geçirilmesi ve bu şekilde zincire eklenmesi sayesinde güvenliğin dağıtık yapılarda nasıl sağlanabileceği konusunda farklı alanlara da bir çok pencere açmıştır.  


Kısaca değinmek üzere başladığım fakat zaman zaman detaya inmek durumunda kaldığım bu yazı ile amacım konuya aşina olmayanlara bir fikir verebilmekti. Umarım faydalı olmuştur. Bitcoin, merkezi otoritelerin para üzerindeki müdahalesi ve transferlerin bir merkezden yönetilmesi süreçlerine alternatif olarak kullanıma sunulmasının üzerinden geçen yıllar sonrasında bir çok ortamda yaygınlaşmaya devam etmekte. Bitcoin ile başlayan ve yaygınlaşan kripto para dünyasına açtığı pencere ile de finansal teknolojinin değişim sürecine katkıda bulunmaya devam etmektedir.  

Özellikle Blockchain teknolojisi ile birlikte yakın gelecekte sağlık sektöründen sigortacılık sektörüne bunun yanında smart contract yapıları ile alım satım veya kontrat işlemlerini içeren farklı çözümler görmeye başlayacağız.  

Önceden tanımlanmış ve koşullar sağlandığında çalışmak üzere kurulu bekleyen işlemlerin/süreçlerin sunulduğu esnek mimarilerin kullanıma açılması da hayatımıza ilk aşamada girmesi beklenen gelişmeler olarak sıralanabilir. Sonuç olarak Blockchain teknolojisi zaman içinde yaygınlaşarak çeşitlenecektir ve daha farklı alanlarda kullanıma açılacaktır.  


  
    

Engin ÜNAL
