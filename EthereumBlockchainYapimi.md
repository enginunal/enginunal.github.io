[Ana Sayfa](https://enginunal.github.io/)

# Kendi Ethereum Blockchain’imizi Yapıyoruz  


Önceki yazımda ethereum ve smart contracts konusunda bazı bilgiler vermiştim. Bu yazıda ise kendimize ait özel ethereum blockchain oluşturup işin pratiğine girmeye başlayacağız. Öncelikle ethereum blockchain oluşturmamızda tüm işi yüklenen Geth isimli bir CLI(Command Line Interface) aracı ile başlayalım.  

Geth, go diliyle yazılmış bir uygulamadır ve ethereum blockchain üzerinde bir çok işlem yapabilmemize olanak sağlar. Geth ile ethereum üzerinde gerçekleştirilebilecek neler var sorusuna; Mandecilik, para transferleri, smart contract işlemleri, blokların sorgulanması gibi bir çok işlem yanıtı verilebilir. Geth gerçek ethereum ağına bağlı veya test ethereum ağınızda çalıştırılabilir. Bu yazıda geth ile test ethereum blockchain’imizi oluşturacağız.   


Öncelikle geth’in bilgisayarınıza yüklenmesi gerekmekte. Bunun için ise kullandığınız işletim sistemine göre bazı adımları izlemeniz gerekmekte. Yazıyı uzatmamak için buraya bunları eklemiyorum, yandaki linkten https://github.com/ethereum/go-ethereum/wiki/Building-Ethereum kurulumu gerçekleştirebilirsiniz. Yazıyı yazarken kullandığım işletim sistemi Windows olduğundan Windows komut satırı çıktısı üzerinden devam edeceğim.   

Kurulumu tamamladıktan sonra ilk olarak kendimize bir klasör açalım. Ve klasör içine girip genesis.json dosyası oluşturalım. dosyanın ismi önemli değil myTest.json da olabilir.   

```
>mkdir myEth
>cd myEth
>echo.>genesis.json
```

genesis.json dosyası yeni oluşturacağımız ethereum blockchain için başlangıç noktası olacaktır. Blockchain, ilk blok olan genesis block’tan itibaren yeni gelen blokları birbirine ekleyerek büyümeye devam edecek ve bu şekilde yapımızı kuracağız. genesis.json içeriği aşağıdaki gibi değiştirilip kaydedilir.  

```
{
  "config": {
    "chainId": 12345,
    "homesteadBlock": 0
  },
  "alloc": {},
  "coinbase": "0x0000000000000000000000000000000000000000",
  "difficulty": "0x20000",
  "extraData": "",
  "gasLimit": "0x2fefd8",
  "nonce": "0x0000000000000042",
  "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "timestamp": "0x00"
}
```

Buradaki config, blockchain konfigurasyon tanımlarını içerir. chainId, replay attack’a karşı koruma amacıyla kullanılmaktadır. homesteadBlock, ethereum’um ikinci büyük versiyonudur, sıfır geçildiğinde bunu kullanır. difficulty, mining işleminin zorluğunu tanımlar. gasLimit, blok başına gaz maliyetinin limiti.   

Oluşturma işlemine devam ediyoruz. Artık geth ile blockchain oluşturabiliriz. datadir olarak blockchain’in oluşturulacağı klasörü belirleyip, init ile başlangıç noktamız olan genesis.json dosyasını gösteriyoruz.  
  
```
>geth --datadir "c:\myEth" init "genesis.json"
```


Sonuç çıktısı:  

```
WARN [02-16|16:02:55] No etherbase set and no accounts found as default
INFO [02-16|16:02:55] Allocated cache and file handles         database=c:\\myEth\\geth\\chaindata cache=16 handles=16
INFO [02-16|16:02:55] Writing custom genesis block
INFO [02-16|16:02:55] Successfully wrote genesis state         database=chaindata                  hash=5e1fc7d790e0
INFO [02-16|16:02:55] Allocated cache and file handles         database=c:\\myEth\\geth\\lightchaindata cache=16 handles=16
INFO [02-16|16:02:55] Writing custom genesis block
INFO [02-16|16:02:55] Successfully wrote genesis state         database=lightchaindata                  hash=5e1fc7d790e0
```
  
Evet ethereum blockchain hazır, artık buna bağlanıp hesap açma veya mining işlemlerine başlayabiliriz. Geth bize bu tip işlemlerin yapılabilmesi için javascript tabanlı bir konsol sunuyor. Bunu açmak için aşağıdaki komutu kullanacağız. Bu komut içinde geçtiğimiz parametrelerin anlamı ise nodiscover: blockchain’imizi manuel olarak eklemeyenler tarafından keşfedilemediğinden emin olmak için kullanılır ve bilgimiz dışında eklenilmesini engeller, ipcdisable: IPC-RPC sunucusunu devre dışı bırakır.  
Bunun gibi bir çok parametre mevcut bunların kullanımı ve açıklamaları https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options linkinden öğrenilebilir.  
  
Konsolu açalım.  

```
>geth --datadir "c:\myEth" --ipcdisable --nodiscover  console
```

Sonuç çıktısı:  
```
WARN [02-16|16:07:32] No etherbase set and no accounts found as default
INFO [02-16|16:07:32] Starting peer-to-peer node instance=Geth/v1.7.3-stable-4bb3c89d/windows-amd64/go1.9
INFO [02-16|16:07:32] Allocated cache and file handles database=c:\\myEth\\geth\\chaindata cache=128 handles=1024
WARN [02-16|16:07:32] Upgrading database to use lookup entries
INFO [02-16|16:07:32] Database deduplication successful        deduped=0
INFO [02-16|16:07:32] Initialised chain configuration          config="{ChainID:12345 Homestead: 0 DAO: <nil> DAOSupport: false EIP150: <nil> EIP155: <nil> EIP 158: <nil> Byzantium: <nil> Engine: unknown}"
INFO [02-16|16:07:32] Disk storage enabled for ethash caches   dir=c:\\myEth\\geth\\ethash count=3
INFO [02-16|16:07:32] Disk storage enabled for ethash DAGs dir=C:\\Users\\ZZZ\\AppData\\Ethash count=2
INFO [02-16|16:07:32] Initialising Ethereum protocol           versions="[63 62]" network=1
INFO [02-16|16:07:32] Loaded most recent local header          number=0 hash=5e1fc7d790e0 td=131072
INFO [02-16|16:07:32] Loaded most recent local full block      number=0 hash=5e1fc7d790e0 td=131072
INFO [02-16|16:07:32] Loaded most recent local fast block      number=0 hash=5e1fc7d790e0 td=131072
INFO [02-16|16:07:32] Regenerated local transaction journal    transactions=0 accounts=0
INFO [02-16|16:07:32] Starting P2P networking
INFO [02-16|16:07:32] RLPx listener up                         self="enode://d30bf920f888b93f76a44e33400cbfe3b3ca53bcfcdff46fd94ebb3734f306ca39943c1d446d90bd045e5a1150ec4eaf41252af22ee63d8edb4074e8edc4accf@[::]:30303?discport=0"
Welcome to the Geth JavaScript console!

instance: Geth/v1.7.3-stable-4bb3c89d/windows-amd64/go1.9
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

> _
```

Artık javascript konsol içerisindeyiz. İlk olarak bir hesap açalım. Hesap açma işleminde bize hesaba atayacağımız şifreyi soracak bunu iki kez giriyoruz ve hesabı oluşturup tanımlama numarasını dönüyor..  

```
> personal.newAccount()
Passphrase:
Repeat passphrase:
"0xb89ac41745b5238cc21fdc3c8704c172197f9a83"
>
```

Konsolu kullanırken otomatik tamamlama özelliği için tab tuşunu kullanabilirsiniz örneğin pe yazıp tab’ladığınızda bunu personal’e tamamlar ve tab ile devam ettiğinizde personal altındaki fonksiyon listesini dönecektir. Şimdi oluşturduğumuz hesabı kontrol için hesap listesini alalım.  

```
> personal.listAccounts
["0xb89ac41745b5238cc21fdc3c8704c172197f9a83"]
```

Sadece tek hesap olduğundan biraz önce açtığımız hesap bilgisini dönmüş oldu.   

eth ile mining işlemleri, hesaptaki para ile ilgili işlemler, blok işlemleri veya transaction gibi bir çok işlem gerçekleştirilebilir. Öncelikle ethereum blockchain’imizdeki blok numarasını alalım.  

```
> eth.blockNumber
```

Sonuç olarak sıfır dönecektir. Henüz mining yapmadığımızdan genesis bloğumuzdan başka bir blok yok. Genesis blok bilgilerine ulaşıp inceleyelim.  

```
> eth.getBlock(0)
```

Sonuç çıktısı:  

```
{
  difficulty: 131072,
  extraData: "0x",
  gasLimit: 3141592,
  gasUsed: 0,
  hash: "0x5e1fc79cb4ffa4739177b5408045cd5d51c6cf766133f23f7cd72ee1f8d790e0",
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  miner: "0x0000000000000000000000000000000000000000",
  mixHash: "0x0000000000000000000000000000000000000000000000000000000000000000",

  nonce: "0x0000000000000042",
  number: 0,
  parentHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
  receiptsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: 507,
  stateRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  timestamp: 0,
  totalDifficulty: 131072,
  transactions: [],
  transactionsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  uncles: []
}
```


Açtığımız hesapta henüz bir eth yok, bunu kontrol etmek için:  

```
>eth.getBalance("0xb89ac41745b5238cc21fdc3c8704c172197f9a83")
```

Sonucu sıfır dönecektir. Biraz para kazanmak için mining yapmaya başlamalıyız. Mining işlemi komutu miner seti altında bulunmakta.   

```
>miner.start(1)
``` 

Komutuyla mining işlemine başlıyoruz, bu işlem ilk çalıştırmada biraz uzun sürebilir. Bir süre bekledikten sonra DAG procesi tamamlanacak ve yeni bloklar mining edilmeye başlanacaktır. blockNumber ile üretilen blok numarası kontrol edilebilir.  

```
>eth.blockNumber
```

Artık blok numarası olarak sıfır değil örneğin 37 dönmekte. Mining işlemini durduralım.  

```
>miner.stop()
```

Hesabımızdaki miktarı kontrol edelim:  

```
>eth.getBalance(eth.accounts[0])
185000000000000000000
```


Artık hesabımızda sıfırdan büyük bir miktarı görmüş olduk. Tabi bu wei olarak listelenmekte bunu ether’e çevirmek için aşağıdaki komut kullanılabilir.  

```
>web3.fromWei(eth.getBalance(eth.accounts[0]), "ether")
185
```

185 ether’imiz olduğunu gördük ve bunu mining yaparak kazandık, son mining işleminin kim tarafından yapıldığını görebilmek için komut ise:  

```
> eth.getBlock(eth.blockNumber).miner
"0xb89ac41745b5238cc21fdc3c8704c172197f9a83"
```

Şimdi bir hesap daha açalım, açtığımız bu hesaba ilk hesabımızdan para gönderimi gerçekleştireceğiz. Öncelikle yeni hesabı açalım.  

```
> personal.newAccount()
Passphrase:
Repeat passphrase:
"0xf57719cabb2cd9b02f8df48f34ca91da0afce58a"
```

İlk açtığımız ve ether’e sahip hesaptan yeni açtığımız hesaba transferi gerçekleştirelim. Transferden önce ilk hesaptaki kilit işlemini kaldırmamız gerekmekte. İlk işlemden önce unlockAccount yaparak hesap üzerindeki transaction kilidini kaldıralım.  

```
>personal.unlockAccount(eth.accounts[0])
Unlock account 0xb89ac41745b5238cc21fdc3c8704c172197f9a83
Passphrase:
true
```


Evet kilidi kaldırmış olduk, şimdi gönderimi gerçekleştirelim.  

```
>eth.sendTransaction({from: eth.accounts[0], to: eth.accounts[1], value: web3.toWei(85,"ether")})
```


İşlem alındı :  
```
INFO [02-16|17:15:48] Submitted transaction                    fullhash=0x853c8524d4ee4be6c2edd128a8542de5c3eae04af16624dad8c74a0e43fc8eac recipient=0xf57719cabb2cD9b02f8df48F34Ca91DA0aFcE58a
"0x853c8524d4ee4be6c2edd128a8542de5c3eae04af16624dad8c74a0e43fc8eac"
```

Buradaki önemli nokta bu işlemin blockchain’e eklenip gerçekleşmesi için miner’lar tarafından işlenmesi gerekiyor bunun için mining yapmalıyız. Tek thread ile mining yapalım.  

```
>miner.start(1)
```

Sonuç çıktısı:  
```
INFO [02-16|17:18:33] Updated mining threads                   threads=1
INFO [02-16|17:18:33] Transaction pool price threshold updated price=18000000000

INFnOu ll[02-> 16|17:18:33] Starting mining operation
INFO [02-16|17:18:33] Commit new mining work                   number=38 txs=1 uncles=0 elapsed=1.000ms
INFO [02-16|17:18:36] Successfully sealed new block            number=38 hash=938a8dba39f6
INFO [02-16|17:18:36] ?? block reached canonical chain          number=33 hash=033a5d2dc30b
```

ve mining işlemini durduralım.  

```
>miner.stop()
```
Mining işlemi çıktısında görüldüğü üzere transaction’ımız blockchain’e eklendi. txs=1 ile bu görülebilir. Transfer işlemimiz gerçekleşip kayda girdiğine göre kontrol edelim. ilk hesap ve ikinci açtığımız hesaptaki miktar bilgileri:  

```
> eth.getBalance(eth.accounts[0])
120000000000000000000
> eth.getBalance(eth.accounts[1])
85000000000000000000
```


İlk hesaptan 85 ether ikinci hesaba geçmiş fakat ilk hesapta bir tuhaflık var gibi gözüküyor. Bunun nedeni ilk hesapla mining yaptığımızdan onun para kazanmaya devam etmesi olarak açıklanabilir.  

Buraya kadar olan bölümü özetlersem. Kendimize ait bir ethereum blockchain oluşturup çalıştırdık. Komut satırı ile hesap açtık. Mining yaparak para kazandık ve bunu görüntüledik. İkinci bir hesap açıp buna para gönderimi gerçekleştirdik yani transaction ürettik. Hesaplardaki miktarların aktarıldığını gözlemledik.   

Şimdiki bölümde ise başka bir ortamdan bizim blockchain’imize nasıl bağlantı kurabiliriz bunu göreceğiz. Öncelikle açtığımız node’daki gereken bilgileri alalım bunun için :  

```
>admin.nodeInfo

{
  enode: "enode://d30bf920f888b93f76a44e33400cbfe3b3ca53bcfcdff46fd94ebb3734f306ca39943c1d446d90bd045e5a1150ec4eaf41252af22ee63d8edb4074e8edc4accf@[::]:30303?discport=0",
  id: "d30bf920f888b93f76a44e33400cbfe3b3ca53bcfcdff46fd94ebb3734f306ca39943c1d446d90bd045e5a1150ec4eaf41252af22ee63d8edb4074e8edc4accf",
  ip: "::",
  listenAddr: "[::]:30303",
  name: "Geth/v1.7.3-stable-4bb3c89d/windows-amd64/go1.9",
  ports: {
    discovery: 0,
    listener: 30303
  },
  protocols: {
    eth: {
      difficulty: 5544451,
      genesis: "0x5e1fc79cb4ffa4739177b5408045cd5d51c6cf766133f23f7cd72ee1f8d790e0",
      head: "0x5b10ff3616c4764acf00c8a75e645ed057d71719912abca6c3cf3b8133c762f3"
,
      network: 1
    }
  }
}
```

Burada görüldüğü üzere network Id değerimiz 1 ve port değerimiz 30303.  İkinci node için bu portla çakışmayacak bir değer seçeceğiz.  

Komut satırımız arkada açık kalsın yeni bir komut satırı açıp myEth2 isminde bir klasör yaratalım ve içindeyken aşağıdaki komutu çalıştıralım.  

```
>geth --datadir "c:\myEth2" init "c:\myEth\genesis.json"
```

Devamında konsolu açalım:  

```
>geth --datadir "c:\myEth2" --ipcdisable --nodiscover --networkid 1 --port 30304 console
```

ilk node’umuza bu node’u peer olarak eklemek için enode değerini alalım  

```
>admin.nodeInfo.enode
"enode://38ebad7cc6ae9434e68d69c06508862300aad05ec2efe7a5176d0ab47c278a01bdfa6b7
2889f02ec507f39d9127b90397f217c20f7ebe8a7569547ddf6f1cebf@[::]:30304?discport=0"
```

Peer olarak ekleme işlemine başlayabiliriz. Bunun için ikinci node’umuzun enode değerini kopyalayalım ve ilk konsolumuzda admin.addPeer ile ekleme işlemini tamamlayalım.  

```
node 1 konsol >admin.addPeer("enode://38ebad7cc6ae9434e68d69c06508862300aad05ec2efe7a5176d0ab47c278a01bdfa6b7
2889f02ec507f39d9127b90397f217c20f7ebe8a7569547ddf6f1cebf@[::]:30304?discport=0")
```

Bu işlem sonrasında ikinci node’umuz blockchain senkronizasyonuna başlar, işlem biraz vakit alabilir. myEth2 klasöründe dosyaların senkronizasyonu takip edilebilir. Bundan sonra ilk node üzerinde yaptığımız tüm transaction’lar ikinci node’a da aktarılacak ve ikisi senkron çalışacaktır.   
Peer ekleme işlemini yaptık, aşağıdaki komutla kontrol edelim:  

```
node 1 konsol >> admin.peers
[{
    caps: ["eth/63"],
    id: "38ebad7cc6ae9434e68d69c06508862300aad05ec2efe7a5176d0ab47c278a01bdfa6b72889f02ec507f39d9127b90397f217c20f7ebe8a7569547ddf6f1cebf",
    name: "Geth/v1.7.3-stable-4bb3c89d/windows-amd64/go1.9",
    network: {
      localAddress: "127.0.0.1:32802",
      remoteAddress: "127.0.0.1:30304"
    },
    protocols: {
      eth: {
        difficulty: 131072,
        head: "0x5e1fc79cb4ffa4739177b5408045cd5d51c6cf766133f23f7cd72ee1f8d790e0",
        version: 63
      }
    }
}]
```

```
node 2 konsol >> admin.peers
[{
    caps: ["eth/63"],
    id: "d30bf920f888b93f76a44e33400cbfe3b3ca53bcfcdff46fd94ebb3734f306ca39943c1d446d90bd045e5a1150ec4eaf41252af22ee63d8edb4074e8edc4accf",
    name: "Geth/v1.7.3-stable-4bb3c89d/windows-amd64/go1.9",
    network: {
      localAddress: "127.0.0.1:30304",
      remoteAddress: "127.0.0.1:32802"
    },
    protocols: {
      eth: {
        difficulty: 7121539,
        head: "0x4a1f35e401f9910b5a15667746901684503cbe0b5f6980b41e3c33f7c1ef8009",
        version: 63
      }
    }
}]
```

Görüldüğü üzere iki node da birbirini peer olarak tanımış oldu. Block senkronizasyonu kontrolünü de yapalım, aynı sayıda blok ikinci node’da da mevcut mu?  

```
node 1 konsol > eth.blockNumber
54
node 2 konsol > eth.blockNumber
54
```

Aynı sayıda blok senkron edilmiş görülüyor. Bu testi mining başlatarak da yapabilirsiniz. Örneğin ilk node’dan mining başlatıp ikinci node’daki blockNumber’ın değiştiği görülebilir.  


İkinci yazımı burada sonlandırıyorum. Bu yazıda sadece geth ile bu işlemlerin nasıl yapılabileceği konusuna değindim. Geth haricinde Truffle(http://truffleframework.com/ ) ve  Ganache(http://truffleframework.com/ganache/ ) ‘ın bu işlemler için hangi kolaylıklar getirdiğini de sizin incelemenizi tavsiye ederim. Umarım faydalı bir yazı olmuştur.



Engin ÜNAL
