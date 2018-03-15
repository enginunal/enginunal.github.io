[Ana Sayfa](https://enginunal.github.io/)

# Ethereum Smart Contract Giris

Önceki yazımda ([Kendi Ethereum Blockchain’imizi Yapıyoruz](https://enginunal.github.io/EthereumBlockchainYapimi))
geth kullanarak kendimize ait bir ethereum blockchain oluşturmuştuk. 
Bu blockchain üzerinde birtakım işlemler gerçekleştirdik ve mining yaparak da hesabımızdaki ETH miktarını arttırdık.  
Bu yazıda özel ethereum blockchain'imizde smart contract yazımına gireceğiz. 

Solidity, ethereum smart contract'ları geliştirmemiz için kullanacağımız bir programlama dilidir. 
C++ ve JavaScript dillerine benzer bir yazıma sahiptir. Daha önce programlama yapmış arkadaşlar bu dili zorlanmadan öğrenebilir, 
Meraklısı için bir çok kaynak mevcut, çok çeşitli kanallardan da öğrenilebileceği gibi benim kaynak olarak önerebileceğim adres:  

[https://solidity.readthedocs.io/en/develop/index.html](https://solidity.readthedocs.io/en/develop/index.html)  

Biraz çalışma mantığına girecek olursak, Solidity ile yazdığımız kodlar ki bunlar derlenip bytecode'a çevrilir ve Smart Contract olarak Ethereum Blockchain'e transaction olarak gönderilir. Bu aşamadan sonra Ethereum Virtual Machine(EVM) üzerinde çalışarak kodlandıkları işleri yaparlar. Smart Contract için uygulama ifadesini kullanırsak, uygulamanın her çağrıldığında bir maliyeti olmaktadır. Uygulamanın her durum değişikliğinde ise blockchain'e son durum bilgisi transaction olarak gönderilir.
Durum değişikliğine örnek, Smart Contract içerisindeki durum değişkenlerinden(class property yapısına benzer) birinin değerinin değişmesi olarak gösterilebilir.  
Bu kadar detaya şimdilik girmeden pratik üzerinden gitmek daha anlaşılabilir olmasını sağlayacaktır bu nedenle yazının devamında daha çok ekran çıktısı ve görsellerle anlatmaya çalışacağım.  

Smart Contract yapısı blockchain dünyasına neler getirmiştir?  

1.Nesil blockchain mimarilerinden farklı olarak Ethereum Blockchain, 
getirdiği virtual machine yeniliği sayesinde Blockchain mimarisini Turing Complete 
bir yapıya taşıyarak 2.Nesil Blockchain'in öncülüğünü yapmıştır.  

>Bitcoin'i HTML'e benzetirsek Ethereum EVM ile birlikte Javascript'in getirdiği gibi bir yenilik getirmiştir.
(Bu örnek Cardano projesinin başındaki Charles Hoskinson'dan alıntıdır).  

Solidity ile geliştireceğimiz smart contract için bir IDE gereksinimimiz olacak bunu da Remix ile gerçekleştireceğiz. 
Remix dışında çeşitli editorler de mevcut(Visual Studio, Atom, Vim, IntelliJ, ...). 
isteğe göre diğerleri de kullanılabilir. Solidity ile yazdığımız smart contract kodunu derleyip blockchain'e göndereceğiz.  

Remix, Solidity dili ile Ethereum smart contract'ları oluşturup test edebilmemize imkan tanıyan browser tabanlı bir IDE. 
Online olarak [https://remix.ethereum.org/](https://remix.ethereum.org/) sayfasından kullanabileceğiniz gibi 
offline olarak ta indirip lokalde kullanabilirsiniz. Offline kullanımlar için hazırlanmış bir zip dosyası mevcut 
ve bunu indirip işlemlerimize başlayabiliriz.  

[https://github.com/ethereum/remix-ide/tree/gh-pages](https://github.com/ethereum/remix-ide/tree/gh-pages) 
adresinden remix-ide zip dosyasını indirip içindeki index.html dosyasını bir browser'da açarak editörü 
offline olarak kullanıma başlayabiliriz.  

Test işlemlerimizde kullanacağımız ethereum blockchain olarak önceki yazımda hazırladığımız blockchain'i 
kullanabilirsiniz veya hiç komut satırı işlerine girmeden ganache ile de test işlemlerinde kullanabileceğiniz bir 
blockchain başlatabilirsiniz. Ben bu yazının devamında ganache kullanacağım. Kurulumu ve kullanımı basit olan 
bu görsel aracın linki:  

[http://truffleframework.com/ganache/](http://truffleframework.com/ganache/)  

Önceki yazıdaki gibi geth ile devam etmek isteyenler için geth komutu aşağıdaki gibi olmalıdır. Dikkat ederseniz
rpc eklentisi ile artık blockchain'imize HTTP-RPC server özelliğini de eklemiş oluyoruz. Bu şekilde REST tabanlı uygulamaların 
RPC(Remote Procedure Call) ile blockchain'imize erişmelerine imkan veriyoruz.

```
geth --datadir "c:\myEth" --nodiscover --rpc --rpcport "7545" --rpccorsdomain "*" 
```

Bu yazının devamında ganache kullanacağım için işlemlerimize onunla devam edelim. Ganache kurulduktan sonra ilk açılışta 
10 hesap ve hepsinde 100 ETH tanımlı olarak gelmekte bunları test işlemlerimizde kullanacağız. İlk aşamada tek blok(genesis) içeren blockchain'i oluşturur ve RPC server'ı başlatır ve bağlanılmaya hazır hale gelir.

![image](/images/SmartContractGiris/4.jpg)  

![image](/images/SmartContractGiris/5.jpg)  

![image](/images/SmartContractGiris/6.jpg)  



  



