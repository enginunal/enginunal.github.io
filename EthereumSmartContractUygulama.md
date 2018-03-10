[Ana Sayfa](https://enginunal.github.io/)

# Ethereum Smart Contract Giris

Önceki yazımda ([Kendi Ethereum Blockchain’imizi Yapıyoruz](https://enginunal.github.io/EthereumBlockchainYapimi))
geth kullanarak kendimize ait bir ethereum blockchain oluşturmuştuk. 
Bu blockchain üzerinde birtakım işlemler gerçekleştirdik ve mining yaparak da para kazandık.  
Bu yazıda özel ethereum blockchain'imizde smart contract yazımına gireceğiz. 

Solidity, ethereum smart contract'ları geliştirmemiz için kullanacağımız bir programlama dilidir. 
C++ ve JavaScript dillerine benzer bir yazıma sahiptir. Daha önce programlama yapmış arkadaşlar bu dili zorlanmadan öğrenebilir, 
internette bir çok kaynak mevcut. Solidity öğrenmek isteyenler için kaynak olarak önerebileceğim adres:  

[https://solidity.readthedocs.io/en/develop/index.html](https://solidity.readthedocs.io/en/develop/index.html)  

Solidity ile yazdığımız kodlar bytecode'a çevrilip blockchain'e transaction olarak gönderilir ve bunlar
ethereum virtual machine(EVM) üzerinde çalışarak görevlerini yerine getirirler.   

>1.Nesil blockchain mimarilerinden farklı olarak Ethereum Blockchain, 
getirdiği virtual machine yeniliği sayesinde Blockchain mimarisini Turing Complete 
bir yapıya taşıyarak 2.Nesil Blockchain'in öncülüğünü yapmıştır. 
Bitcoin'i HTML'e benzetirsek Ethereum EVM ile birlikte Javascript'in getirdiği gibi bir yenilik getirmiştir.
(Bu örnek Cardano projesinin başındaki Charles Hoskinson'dan alıntıdır).  

Bu yazıda solidity kodlamasının detayına girmeden smart contract geliştirmek ve yayınlamak için hangi araçlar kullanılır 
konuları üzerinde duracağım. Bence solidity ile kodlamaya girmeden önce nasıl bir yapıya kod yazıyoruz 
bunu görerek öğrenmek kodlama öğrenimin süresini de kısaltacaktır. Sonraki yazılarımda solidity programlamanın detayına da 
değinmeyi istiyorum.  

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

Bu yazının devamında ganache kullanacağım için işlemlerimize onunla devam edelim. 


To be continued...
