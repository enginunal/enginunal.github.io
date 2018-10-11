[Ana Sayfa](https://enginunal.github.io/)

# Docker Container Ve Swarm Mode

Bu yazıda docker dünyasındaki bileşenler nedir ve nasıl kullanılır konularına değineceğim. Bunu yaparken de uygulamalı yani komut 
örnekleriyle devam edeceğim. Öncelikle docker nedir sanırım bu konuya merak sarmış herkes biliyor o yüzden tarihçe ve tanım kısımlarını
geçiyorum.  

ilk olarak image ve container kavramlarından başlayayım. image bir container'ın oluşması için gereken tüm içeriğin depolandığı 
yapılardır. Programcılar için kısaca container bir instance olarak düşünülebilir, image ise instance'ın yaratıldığı kaynak 
yani class'tır. Veya diğer bir anlatımla image bir container'ı oluşturabilmek ve çalıştırabilmek için gerekli tüm elemanları 
içeren depolardır.  

Container, image kullanılarak yaratılır ve aynı image'dan yaratılmış tüm container'lar hangi platformda olurlarsa olsunlar 
aynı şekilde çalışırlar farklılık göstermezler. Bu aslında geliştirme, deneme ve yayınlama süreçleri için büyük bir kolaylık sağlar. 
Bir image üretip sonrasında container oluşturup testlerimizi gerçekleştirdiğimizde bu image'dan oluşan container'ların yayınlandıktan 
sonra farklı davranma gibi bir şansları olamayacağından müşteri destek ekibini arayıp hata bildirimi yaptığında geliştirme ekibinin 
"ama aynı şeyi biz de denedik bizde çalışıyordu" yanıtını dönmesini engelleyecek bir ortam sağlar.Container yapılarının faydasını 
kısa tutup hemen nasıl kullancağız ona değineyim.  
  

Docker registry'den bir imaj çekmek için image pull komutu kullanılır. pull komutu ile çekilen imaj sisteme indirilir ve kaydedilir.
Örneğin alpine linux imajını çekmek isteyelim aşağıdaki komut ile docker registry'den alpine linux imajı alınır ve sisteme kaydedilir. 
  
```
docker image pull alpine
```
  
Sistemdeki image listesini almak için image ls komutu kullanılır. Listeden image için size,id,repository gibi bilgiler alınabilir.
  
```
docker image ls
```
  

Sisteme kaydedilmiş bir image'dan yeni bir container yaratılıp çalıştırılması için gereken komut container run komutudur. 
Bu komutla image eğer sistemde mevcut değilse docker registry'den otomatik olarak pull edilir.   
Örneğin daha önce sisteme kaydettiğimiz alpine image'ından container yaratıp çalıştıralım.  
  
```
docker container run alpine 
```
  
  
container run komutu ile alpine image'ına ait bir container oluşturulur ve çalıştırılır. Container, yaptığı işlem sona 
erdiğinde kapanacaktır. Aşağıdaki örnekte ise alpine container çalışsın ve ekrana merhaba yazsın sonrasında işlem sonlandığı 
için kapanacaktır.  
  
```
docker container run alpine echo "merhaba"
```
  

Container içerisindeki shell'e erişip işlem yapmak istiyorsak.  
  
```
docker container run -it alpine /bin/sh
```
  
Komutunu kullanabiliriz, biz shell'den exit ile çıkana kadar container çalışacak ve shell'de kalacaktır. 
shell exit yapıldığında container'da kapatılır.  
Aktif olan veya kapanmış olan tüm container listesini alabilmek için container ls komutu kullanılır. 
Bu komutla sistemdeki container listesini ve durumlarını öğrenebiliriz.  
  
```
docker container ls -a
```
  

id değerini bildiğimiz bir container'ı tekrar çalıştırmak için container start komutu kullanılır. 
Örnek olarak id değeri 17638aba6c37 olan ve şu anda çalışmayan container'ımızı tekrar çalıştıralım.  
  
```
docker container start 17638aba6c37
```
  
  
Çalışan bir container içerisinde komut çalıştırmak istiyorsak container exec komutu kullanılır. Örneğin id değeri 
17638aba6c37 olan ve çalışmakta olan container içerisine ls komutu gönderilerek dosya listesini alalım.  

```
docker container exec 17638aba6c37 ls
```

Veya shell erişimi yapalım.  

```
docker container exec 176 -it alpine /bin/sh
```
  
>Not: container id olarak tüm değerin girilmesine gerek yok, Diğer id'lerle ortak olmayacak şekilde birkaç rakam girmek yeterli.  
  
>Not: Bu konuda karıştırılmaması gereken ve vurgulamak istediğim komutlar container start ve container run komutlarıdır. 
run komutu bir image'dan yeni bir container yaratır. start komutu ise mevcut olan bir container'ı tekrar çalıştırır.  

>Not: container attach komutu ile de çalışan bir container içerisine doğrudan girilebilir. exec komutu ile karıştırılmamalı. 
exec komutu adı üstünde çalışan bir container içerisinde komut çalıştırmak için kullanılır.  
  
  

### Image Oluşturmak  

### 1. Mevcut Bir Container Kullanarak Image Oluşturmak  

Bu konuda docker store'dan ubuntu container'ını çekerek başlayalım. Ubuntu container içerisine girip bash shell komut 
satırına erişeceğiz.  

```
docker container run -ti ubuntu bash
```
  
Sonrasında bu container içerisine cowsay isimli karakter tabanlı eğlenceli uygulamayı yükleyip deneyeceğiz.  

```
apt-get update
apt-get install -y cowsay
cowsay deneme
```
veya 
```
/usr/games/cowsay deneme
```
  
Ekranda aşağıdaki gibi bir çıktımız olacak :  
```
 ________
< deneme >
 --------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
  
Uygulamamız sorunsuz çalışıyor ve denemesini yaptık artık exit komutu ile container'dan çıkıp değiştirdiğimiz container 
üzerinde inceleme yapalım.  

```
docker container ls -a

CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                           PORTS               NAMES
965ade02a6cb        ubuntu              "bash"              About a minute ago   Exited (127) 7 seconds ago                           adoring_bartik
5d4d04be114d        ubuntu              "bash"              About an hour ago    Exited (130) About an hour ago                       hopeful_shtern
```
  
Uygulamayı yüklediğimiz container id'si 965ade02a6cb olarak not alıyoruz. Bu container'da ne gibi değişiklikler yaptığımızı 
görüntülemek için kullanacağımız komut ise diff komutu olacak.   

```
docker container diff 965ade02a6cb
```

Mevcut bir container kullanılarak Image yaratmak için kullanacağımız komut ise commit komutudur. Bu komutla docker engine localde 
bir image yaratacaktır.  

```
docker container commit 965ade02a6cb
```

Image işlemi tamamlandıktan sonra image listesini kontrol edelim.  

```
docker image ls
```

Komut çıktısı:  
```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              3c2d4954f61b        29 seconds ago      168MB
ubuntu              latest              cd6d8154f1e1        4 weeks ago         84.1MB
```

Tag ve repository alanlarının boş geldiği görülebilir. Bu image'a bir tag verelim.  

```
docker image tag 3c2d4954f61b cowsay_deneme_image
docker image ls
  
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
cowsay_deneme_image   latest              3c2d4954f61b        3 minutes ago       168MB
ubuntu                latest              cd6d8154f1e1        4 weeks ago         84.1MB
```
  
Evet sistemimizde bulunan bir container'dan image oluşturmayı tamamladık. şimdi bu image'dan container oluşturup çalıştıralım 
ve çıktısını alalım.  

```
docker container run cowsay_deneme_image cowsay merhaba
  
  
 _________
< merhaba >
 ---------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

```


Sistemdeki container'ları listelersek :  

```
docker container ls -a
  
CONTAINER ID        IMAGE                 COMMAND                  CREATED   STATUS                           PORTS               NAMES
1a34b84869af        cowsay_deneme_image   "cowsay merhaba"         About a minute ago   Exited (0) About a minute ago             festive_bartik
965ade02a6cb        ubuntu                "bash"                   18 minutes ago   Exited (127) 17 minutes ago                   adoring_bartik
5d4d04be114d        ubuntu                "bash"                   About an hour ago   Exited (130) About an hour ago             hopeful_shtern
```

Görüldüğü gibi cowsay_deneme_image image'ından yaratılan container çalıştı ve işlemini tamamlayıp çıkış yapmış oldu.  
  
  
### 2. Dockerfile Kullanarak Image Oluşturmak  

Docker container'larını editleyerek image oluşturma işlemi yönetilmesi zor ve verimli bir yöntem değildir. 
Bunun yerine dockerfile dosyası ile image oluşturma yöntemi tercih edilmektedir. Hazırlanan dockerfile sonrasında docker build komutu
ile image oluşturulur. Küçük bir örnekle bunu inceleyelim.  

Öncelikle oluşturacağımız image içerisine koymak için bir program yazalım. Ben örnek olarak hostname ve username 
bilgisini dönen bir C kodu yazdım.  

```
#include <stdio.h>
#include <unistd.h>
#include <limits.h>

void main(void)
{
  char hostname[HOST_NAME_MAX];
  char username[LOGIN_NAME_MAX];

  gethostname(hostname, HOST_NAME_MAX);
  getlogin_r(username, LOGIN_NAME_MAX);

  printf("Host=%s ve Kull=%s\n", hostname, username);
}
```

Dosyayı derleyip çalıştırlabilir uygulama üretmek için :  

```
gcc -o deneme deneme.c

chmod a+x deneme
```
  
Artık çalıştırlabilir dosyamız hazır. Şimdi Dockerfile dosyasını oluşturalım :  

```
FROM alpine
RUN apk update && apk add gcc
COPY . /app
WORKDIR /app
CMD ./deneme
```

Son olarak docker build komutu ile image dosyasını oluşturalım.  
  
```
docker image build -t deneme:v0.1 .
```

Dosyamız oluştu, bunu image ls komutu ile kontrol edebiliriz.  

```
docker image ls
  
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
deneme              v0.1                cbf9772a6208        3 minutes ago       93.5MB
alpine              latest              196d12cf6ab1        3 weeks ago         4.41MB
```

Artık container'ımızı çalıştırabiliriz. Aşağıdaki komut ile deneme image'ı container olarak yaratılır ve sonucu 
ekrana yazdırarak işlemini sonlandırır.  

```
docker container run deneme:v0.1
  
Host=0fe6f14924f3 ve Kull=
```

```
docker container ls -a 
  
CONTAINER ID        IMAGE               COMMAND                 CREATED             STATUS                     PORTS               NAMES
0fe6f14924f3        deneme:v0.1         "/bin/sh -c ./deneme"   2 minutes ago       Exited (0) 2 minutes ago                       naughty_mirzakhani
```

Uygulamamızdan dönen host bilgisi ile container id değerleri aynı, uygulamamız container içerisinde host edildi ve çalıştı.  
Oluşturduğumuz docker image ile ilgili detaylı bilgi almak istiyorsak :  

```
docker image inspect deneme:v0.1
```

Bu komutla image bilgilerini JSON formatında alabiliriz. Dönen json içerisinde image metadata'sı 
bulunmaktadır. Bu metadata incelendiğinde docker image'ın aslında katmanlı bir yapıya sahip olduğu görülebilir. 
RootFS.Layers bölümünden bu incelenebilir. Docker'un çoklu katman yapısını desteklemesi neticesinde bir image'dan başka 
bir image'ın türetilmesi yani inheritance mümkün olmakta ve daha karmaşık yapıların birbirinin omuzu üzerinde yükselmesi 
imkanı doğmaktadır.  

### Aynı Host Üzerindeki Container Haberleşmesi  

Container'lar arası haberleşme konusuna da kısaca değinmek gerekirse. Tek host olan yapıda host içerisindeki container'lar 
standart olarak kendi aralarında bridge network altyapısı ile haberleşirler. Birbirleriyle haberleşmede herhangi bir 
engele uğramazlar fakat dışarıdan erişilmeye kapalıdırlar bu da kısmen izolasyon anlamına gelir.  
Container'lar istenirse dış dünyadan erişilebilmesi için port açabilir ve bunu host üzerinden publish edebilir. 
Örneğin host altında nginx container'ı başlatalım, dışarıdan 8080 portundan erişilebilir olsun, kullanabileceğimiz komut.  

```
docker container run -p 80:8080 nginx
```

Böylece dışarıya publish ettiğimiz 8080 portuna gelen istek container'ın 80 portuna yönlendirilir.
Bridge network standart olarak yaratılır demiştik, bunun yanında istenirse user-defined(kullanıcı tanımlı) bridge network 
yaratma imkanı da vardır(docker network create -d bridge <isim> komutu ile), container'lar bu network'e dahil 
edilebilir(docker network connect bridge <containerid> komutu ile).  


![image](/images/DockerContainerVeSwarmMode/BridgeNetwork.jpg)  


Mevcut docker host üzerinde bridge network altındaki container'ları incelemek isterseniz komut satırından :  

```
docker network inspect bridge 
```

Komutu çalıştırılarak bridge network'e bağlı container'lar incelenebilir. Networking konusunu uzatmadan devam edip swarm cluster 
mimarisine geçelim.  

  
  
  
## Swarm Mode   

  
Buraya kadar olan bölümde bir sunucu üzerinde bir container oluşturma, düzenleme ve kullanma üzerinde durdum fakat 
gerçek hayatta birden çok sunucu üzerinde çok sayıda container'ın host edildiği ve çok daha karmaşık 
kullanımların olduğu durumlar olacaktır. Ve bu sistemlerin ölçeklenebilir yapılar olması gerekliliği ortaya çıkacaktır.   
Docker container'ların bir orkestratör yardımı ile cluster içerisindeki node'larda yönetilmesi ve bu işlemin otomatize 
edilmesi büyük çaplı sistemlerin yönetilebilmesini kolaylaştırmakta high availability gibi kavramların uygulanabilmesine 
imkan tanımaktadır. Bu gibi konular için container'ların yönetildiği ve orkestre edildiği bir çok çözüm mevcuttur. 
Ama bu yazının konusu docker ürünleri ile ilgili olduğundan docker'ın buna ürettiği çözüm swarm mode olarak ortaya çıkmakta. 
Önceki yazılarımda cluster, node ve bunun gibi kavramlardan bahsetmiştim o nedenle hızlıca docker swarm mode ile ne 
nasıl yapılır anlatıma geçeceğim.  

Swarm mode temel olarak sürekli erişilebilirlik(high availability) ve ölçeklenebilirlik(scalability) sorunlarına
getirdiği kolay kullanımlı ve hızlı çözüm nedeniyle tercih edilmektedir. Kubernetes(k8s) de aynı işlemleri ve daha çok 
seçenekle yapabilmekte fakat öğrenim süresi ve kolay kullanım açısından docker swarm bir adım öne çıkmakta, 
en azından benim düşüncem bu yönde. swarm(yazının devamında docker swarm mode yerine kısaca swarm kullanacağım) 
yapısal olarak iki tip node'dan oluşur, bunlar :  

![image](/images/DockerContainerVeSwarmMode/swarm-diagram.jpg)  

#### Swarm cluster içerisindeki node'lar ikiye ayrılır.  
  
#### 1. Manager Node  

Adı üstünde swarm cluster üzerindeki işlerin yönetilmesini gerçekleştiren node grubudur. Servislerin yönetilmesi, 
ölçekleme, sürekli monitör ederek cluster ortamını(cluster state) istenen seviyede tutma(desired state), 
servisler arası yük dağılımı(load balancing) gibi görevleri vardır. Cluster içerisindeki manager node sayısı high availability 
açısından önemlidir. Split brain gibi senaryoların gerçekleşmesine önlem olarak tek sayıda manager kullanılmalıdır.  
Bir manager'ın çökebilmesi ihtimaline karşı en optime çözüm en az 3 manager kullanılmasıdır. 5 manager varsa iki manager'ın 
çökme riskini elimine eder. Bunu förmüle edersek :  

N manager olan cluster içerisinde (N-1)/2 manager kaybı tolere edilebilir.  

>Not: Docker en fazla 7 manager önermektedir.  

İşlerin dağılımının manager ile gerçekleştirildiğinden bahsetmiştim. İşler hem manager node'larda hem de worker node'larda 
çalışabilir. Eğer istenirse sadece worker node üzerinde çalışacak şekilde tanımlanabilir(drain). 
Bu tasarımınıza göre değişkenlik gösterecektir.  
  

#### 2. Worker Node  

İşlerin yürüdüğü yani container'larımızın çalıştığı node'lara verilen isimdir. Bir swarm cluster'da hiç worker node yokken 
de cluster tüm işlevini yerine getirebilir fakat sadece worker node olan bir cluster olamaz. 
Bir worker node sonradan manager yapılabilir(promote).  
  
  
Artık komut satırından bir swarm cluster oluşturabiliriz. İlk adımda init yaparak yeni bir swarm cluster oluşturacağız. 
Swarm cluster yönetimi ile ilgili komutları çalıştırken docker swarm kullanılır. 
Örnek amaçlı olduğundan 3 manager ve 2 worker için işlemleri tekrarlama gereği olmadığından iki node içeren bir yapı için 
swarm cluster oluşturmak için init yapalım.  
  
```
docker swarm init --advertise-addr $(hostname -i)
  
Swarm initialized: current node (g1wkk2jnoygiahycglr6nlsle) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-0habm68o4lz3g61dxhsfecq6e2nod75o5cz3bej7r4ac8uprjv-0ds7fwaaud8fylqr2z4uidzz2 192.168.0.33:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```
  
Cluster hazır ve ilk node olan manager node oluştu, diğer node'umuzu da worker node olarak ekleyelim. Bunun için init yaptıktan 
sonra dönen açıklama içerisindeki "docker swarm join --token ..." şeklinde devam eden komutu kopyalayıp kullanabiliriz 
veya manager'daki komut satırından "docker swarm join-token worker" ile join token bilgisini alabiliriz. Şimdi ikinci 
node'umuzu worker olarak ekleyelim. Bunun için ikinci node komut satırından  

```
docker swarm join --token SWMTKN-1-0habm68o4lz3g61dxhsfecq6e2nod75o5cz3bej7r4ac8uprjv-0ds7fwaaud8fylqr2z4uidzz2 192.168.0.33:2377
```
Komutu çalıştırılır ve "This node joined a swarm as a worker." yanıtı alındığında artık bir manager bir worker içeren 
swarm cluster hazır. Manager node komut satırından aşağıdaki node ls komutu ile cluster içerisindeki node listesini alınabilir.   

```
docker node ls
  
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
g1wkk2jnoygiahycglr6nlsle *   node1               Ready               Active              Leader              18.03.1-ce
0egcvtjlozki1flq5s4lx2ww4     node2               Ready               Active                                  18.03.1-ce
```
  

Manager status olarak leader gözüken node swarm init yaptığımız ilk node'umuz(node1). Şu anda onun komut satırında 
olduğumuzdan ID kolonunda * işareti bulunmakta. Birden çok manager node var olabilir ama tek leader olur. Eğer leader 
çökerse yeni bir leader manager'lar arasından belirlenir. Bu işlem otomatik gerçekleşir. Yeni leader seçimi nasıl 
gerçekleşir? Raft consensus algoritması kullanılarak bu işlem gerçekleştiriliyor. 
Bu algöritma ile ilgili [http://thesecretlivesofdata.com/raft/](http://thesecretlivesofdata.com/raft/) adresinde basitçe 
anlatılmış tavsiye ederim.  

Cluster oluşturma işlemi tamamlandı ve node'lar eklendi. Şimdi cluster'ımıza 3 adet nginx web sunucu servisi ekleyelim ve 
bunu node'lara nasıl dağıtıldığını inceleyelim. Servis oluşturmak için service create komutu kullanacağız, 
nginx servisimize deneme_web ismini verip 3 tane oluşturmasını isteyeceğiz.  

```
docker service create --name deneme_web --replicas 3 nginx
  
nmqpew9iwfdjei79wsadyy3pw
overall progress: 3 out of 3 tasks
1/3: running
2/3: running
3/3: running
verify: Service converged
```

Bu üç container yani deneme_web servisimiz nerede host ediliyor inceleyelim.   

```
docker service ps deneme_web
  
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE                ERROR               

PORTS
nqyiy4e4pxx9        deneme_web.1        nginx:latest        node2               Running             Running about a minute ago
qmokjrfkxmna        deneme_web.2        nginx:latest        node1               Running             Running about a minute ago
ifqwa75eh3m8        deneme_web.3        nginx:latest        node2               Running             Running about a minute ago
```

İkisi node2'de biri de node1 ye yönlendirilmiş. Şimdi deneme_web servisini scale edip replica sayısını 20 yapalım.  
  
```
docker service scale deneme_web=20
  
deneme_web scaled to 20
overall progress: 0 out of 20 tasks
1/20:
2/20:
overall progress: 20 out of 20 tasks
4/20: running   [==================================================>]
5/20: running   [==================================================>]
6/20: running   [==================================================>]
7/20: running   [==================================================>]
8/20: running   [==================================================>]
9/20: running   [==================================================>]
10/20: running   [==================================================>]
11/20: running   [==================================================>]
12/20: running   [==================================================>]
13/20: running   [==================================================>]
14/20: running   [==================================================>]
15/20: running   [==================================================>]
16/20: running   [==================================================>]
17/20: running   [==================================================>]
18/20: running   [==================================================>]
19/20: running   [==================================================>]
20/20: running   [==================================================>]
verify: Service converged
```

Tekrar servisimizi incelediğimizde bu 20 replikanın hangi node'lara dağıtıldığını görebiliriz.  

```
docker service ps deneme_web
  
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE                ERROR               

PORTS
nqyiy4e4pxx9        deneme_web.1        nginx:latest        node2               Running             Running 4 minutes ago
qmokjrfkxmna        deneme_web.2        nginx:latest        node1               Running             Running 4 minutes ago
ifqwa75eh3m8        deneme_web.3        nginx:latest        node2               Running             Running 4 minutes ago
r5bf18czv86h        deneme_web.4        nginx:latest        node2               Running             Running about a minute ago
n8cp86oa0f66        deneme_web.5        nginx:latest        node1               Running             Running about a minute ago
22x0gm52tcxe        deneme_web.6        nginx:latest        node2               Running             Running about a minute ago
lup9je43mthk        deneme_web.7        nginx:latest        node1               Running             Running about a minute ago
4u60xzahxoaq        deneme_web.8        nginx:latest        node2               Running             Running about a minute ago
fcvwhrqlsx9v        deneme_web.9        nginx:latest        node2               Running             Running about a minute ago
5v07hoyey5yh        deneme_web.10       nginx:latest        node2               Running             Running about a minute ago
450s0uz9bt2i        deneme_web.11       nginx:latest        node1               Running             Running about a minute ago
tr2ae2afvhzg        deneme_web.12       nginx:latest        node1               Running             Running about a minute ago
ihvvo28k8jhk        deneme_web.13       nginx:latest        node1               Running             Running about a minute ago
m3i2ozt7a1le        deneme_web.14       nginx:latest        node2               Running             Running about a minute ago
k3o7mab28lyh        deneme_web.15       nginx:latest        node1               Running             Running about a minute ago
uad7tnicfnid        deneme_web.16       nginx:latest        node1               Running             Running about a minute ago
wp7xoalheog9        deneme_web.17       nginx:latest        node1               Running             Running about a minute ago
fa89egxq4bl3        deneme_web.18       nginx:latest        node2               Running             Running about a minute ago
qt8if8o319uh        deneme_web.19       nginx:latest        node1               Running             Running about a minute ago
ufa899m5r26g        deneme_web.20       nginx:latest        node2               Running             Running about a minute ago
```
  
Oluşturulan container'lar node1 ve node2 arasında scale edilerek dağıtıldı. Bu ve bunun gibi örnekleri artırabiliriz 
sonuç olarak bir servisin scale edilmesinin swarm tarafında nasıl kolaylaştırıldığının altını çizmek gerekiyor.  

Şimdi stack, service ve task kavramlarına bakalım. Task, swarm içerisinde container ve container içerisinde çalıştırılacak 
komutlara verilen isimdir. Kısaca bir container instance'ı olarak özetlenebilir. Bir task node'a atandığında başka bir 
node'a kaydırılamaz sadece o node üzerinde çalışır veya hata verip iptal olur. Service, çalışacak task 
tanımının bulunduğu yapıdır. Service tanımı o servisin hangi container image'ını kullanacağını, container içerisinde 
hangi komutun çalışacağını, kaç adet replika task(container) içereceğini, port tanımı vb. tanımları içerir. Bir service 
deploy edildiğinde swarm manager servis tanımlamasına bakarak task'lerin dağılımını ve çalıştırılmasını node'lar 
üzerinde organize eder. Stack ise birbiriyle ilişkili veya paylaşımlı servis gruplarının tanımlandığı yapıdır. Stack ile 
baştan aşağıya tüm uygulama deploy edilebilir, servis tanımlamalarının bulunduğu bir yml dosyasıdır, 
böylece docker service create gibi komutlar ile uğraşmak yerine tek bir dosyadan servis mimarimizi, 
kaç instance olacağını veya bunların birbirine nasıl bağlanacağını tanımlayabiliriz.   

Şimdi docker github sayfasındaki temel örneklerden biri olan oylama 
uygulamasını(https://github.com/docker/example-voting-app) oluşturduğumuz swarm cluster'a deploy edelim.  

docker-stack yml dosyası :  

```
cat docker-stack.yml
  
  
version: "3"
services:

  redis:
    image: redis:alpine
    ports:
      - "6379"
    networks:
      - frontend
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure
  db:
    image: postgres:9.4
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - backend
    deploy:
      placement:
        constraints: [node.role == manager]
  vote:
    image: dockersamples/examplevotingapp_vote:before
    ports:
      - 5000:80
    networks:
      - frontend
    depends_on:
      - redis
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
      restart_policy:
        condition: on-failure
  result:
    image: dockersamples/examplevotingapp_result:before
    ports:
      - 5001:80
    networks:
      - backend
    depends_on:
      - db
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure

  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - frontend
      - backend
    deploy:
      mode: replicated
      replicas: 1
      labels: [APP=VOTING]
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
      placement:
        constraints: [node.role == manager]

  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    stop_grace_period: 1m30s
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]

networks:
  frontend:
  backend:

volumes:
  db-data:
```

Uygulamayı voting_stack ismiyle deploy edeceğiz, bunun için docker stack deploy komutu kullanılır.  

```
docker stack deploy --compose-file=docker-stack.yml voting_stack
  
Creating network voting_stack_frontend
Creating network voting_stack_backend
Creating network voting_stack_default
Creating service voting_stack_redis
Creating service voting_stack_db
Creating service voting_stack_vote
Creating service voting_stack_result
Creating service voting_stack_worker
Creating service voting_stack_visualizer
```

docker stack ls komutuyla incelersek :  

```
NAME                SERVICES
voting_stack        6
```

Altı servisin voting_stack uygulaması için deploy edildiği görülebilir. Stack altındaki her servisi services 
komutu ile inceleyebiliriz.  

```
docker stack services voting_stack
  
ID                  NAME                      MODE                REPLICAS            IMAGE                                          PORTS
085hhhzv9law        voting_stack_db           replicated          1/1                 postgres:9.4
ch2go0fwdo1c        voting_stack_result       replicated          1/1                 dockersamples/examplevotingapp_result:before   *:5001->80/tcp
ibo7nnlp84vr        voting_stack_vote         replicated          2/2                 dockersamples/examplevotingapp_vote:before     *:5000->80/tcp
k43elnoymz8u        voting_stack_redis        replicated          1/1                 redis:alpine                                   *:30000->6379/tcp
m6ldv8swkm7c        voting_stack_worker       replicated          1/1                 dockersamples/examplevotingapp_worker:latest
mx41xguxk98m        voting_stack_visualizer   replicated          1/1                 dockersamples/visualizer:stable                *:8080->8080/tcp
```

Görüldüğü üzere voting_stack_vote yani oy vereceğimiz uygulama servisinden 2 adet replike edilmiş. Bu servisi incelersek.  

```
docker service ps voting_stack_vote
  
ID                  NAME                  IMAGE                                        NODE                DESIRED STATE       CURRENT STATE           

ERROR               PORTS
340shdx4iqfz        voting_stack_vote.1   dockersamples/examplevotingapp_vote:before   node2               Running             Running 5 minutes ago
e808iz3r2w4y        voting_stack_vote.2   dockersamples/examplevotingapp_vote:before   node1               Running             Running 5 minutes ago
```

Bir task node2 üzerinde diğeri de node1 üzerinde görülüyor. Uygulamayı çalıştırıp oy vermek ve verilen oyları 
görüntülemek için swarm ip adresine, oylama yapmak için port:5000, oy sonuçları için port:5001 ve swamr cluster 
durumunu inceleyebileceğiniz visualizer uygulamasına erişmek için port:8080 kullanılabilir.   
Bu bilgileri stack yml dosyasında da bulabilirsiniz.  


Oy verme ekranı :  

![image](/images/DockerContainerVeSwarmMode/swarm-vote.jpg)  


Oy sonuçları ekranı :  

![image](/images/DockerContainerVeSwarmMode/swarm-vote-result.jpg)  


Swarm cluster visualizer ekranı:

![image](/images/DockerContainerVeSwarmMode/swarm-visualizer.jpg)  


Cluster'ı izlemek için denemenizi önerebileceğim diğer uygulama da [portainer](https://portainer.io).  
Oylama uygulamasını içeren swarm cluster'ımıza bir portainer servisi kurduğumuzda portainer ekran görüntüleri :  


![image](/images/DockerContainerVeSwarmMode/swarm-portainer-cluster.jpg)  
  
![image](/images/DockerContainerVeSwarmMode/swarm-portainer-cluster-services.jpg)  
  
  



### Networking  

Biraz önce servis oluşturduk ve scale ettik, container'ların bazıları node1 de iken bazıları node2'de oluştu, 
oluşturulan container'lar farklı node'lara nasıl dağıtılabiliyor ve aralarındaki haberleşme nasıl gerçekleşiyor? 
Aslında docker networking konusu ayrı bir yazı konusu olacak kadar önemli ve detaylı bir konu belki sadece bu konuyu 
içeren bir yazı hazırlamak iyi olur fakat bu yazıda kısaca da olsa değineceğim.  
Docker'ın container'lar arasında bağlantıyı sağlayan çözümü overlay network mimarisidir. Temelinde linux kernel bridge 
yapısını ve container haberleşmesi için de VXLAN(virtual extensible lan) tünellemesini kullanıyor. VXLAN ile 
alttaki network'ten(underlay) bağımsız bir katman oluşturup(overlay) container'ların haberleşmelerini bu 
katmanda gerçekleştiriyor. Kabaca şöyle düşünebiliriz; Telefon hatları underlay network ise internet overlay network denilebilir.   

  
![image](/images/DockerContainerVeSwarmMode/overlayNetwork.jpg)  
  

Birkaç cümle ile daha açıklamak gerekirse; VXLAN tünellemesi ile layer3 network altyapısı üzerinde bir 
virtual layer 2 network mimarisi oluşturuluyor. Her VXLAN tüneli VTEP denilen yapılarda sonlanıyor. 
VTEP ise vxlan tunnel endpoint'in kısaltması. İşte tüm işleri bu VTEP yapmakta. VTEP'ler node'lar arasında VXLAN tünellerini 
kullanarak overlay network yapısının gerçekleşmesini sağlıyor. Overlay network izole bir network yani overlay 
içerisindeki bir container'a o network dışından erişilemiyor. Bu da aslında çok kullanışlı ve güvenli yapıların 
tasarımlanması için imkanlar doğurmakta. Birbirinden habersiz ve bağımsız overlay network'ler içerisinde çalşan katmanlı 
tasarımların gerçekleşmesi bu sayede oldukça kolaylaşıyor. Aşağıdaki şemada bununla ilgili güzel bir gösterim de mevcut.  

  
![image](/images/DockerContainerVeSwarmMode/overlay_vxlan_detail.jpg)  
  

Gelelim swarm cluster'da neler olduğuna, swarm cluster oluşturduğunuzda iki network tipi yaratılıyor. 
Biri ingress adı verilen ve swarm servislerinin haberleşmesinde kullanılan bir overlay network diğeri ise docker_gwbridge 
adı verilen ve tüm overlay network'leri(ingress de dahil) birbirine bağlamak için sanal bir köprü(virtual bridge) 
olarak kullanılan bridge network. Bu yapılar kullanılarak ve load balancer dahil edilerek ulaşılan son nokta ise routing mesh. 
Routing mesh, swarm içerisindeki servislerde publish edilen portların dışarıdan kolayca erişilebileceği bir yapı 
sunmaktadır, load balancer sayesinde gelen isteğin iletileceği container seçiminde yük dağılımına göre davranır.   

  
![image](/images/DockerContainerVeSwarmMode/ingress-routing-mesh.jpg)  
  

Cluster içerisinden dışarı publish edilmiş bir porta gelen istek alınır, hangi node'daki hangi container 
daha ulaşılabilir ve sağlıklı durumda ise load balancer ile ona yönlendirilir. Diyelim ki 2 manager + 2 worker 
içeren swarm cluster'ımız olsun. IP adresleri örnek şemadakine uyması açısından 
192.168.99.100, 192.168.99.101, 192.168.99.102 olsun. 
Bu cluster'da my-web adında bir nginx servisi yaratalım, container'ın iki replikası olsun ve 
nginx dışarı 8080 portundan çıksın.  
  
```
docker service create --name my-web --publish 8080:80 --replicas 2 nginx
```
  

Örnek resimde node1 ve node2 my-web container'larını barındırıyor fakat node3 üzerinde container yok. node1, node2 veya 
node3 farketmez hangisinin IP adresine port 8080 üzerinde istekte bulunursak bulunalım eğer node'lardan herhangi 
birinde bu portu publish eden bir container varsa yönlendirme ona yapılır ve nginx sayfası görüntülenir.   

Örneğin 192.168.99.102:8080 http request'i yaptığımızda aktif olan container'a yönlendirme yapılır. Yani routing mesh, 
swarm içinde bulunan tüm node'ların publish edilmiş herhangi bir porta bağlantı isteğini kabul eder ve 
içerideki en uygun node üzerindeki container'a(load balancer ile) yönlendirmesini yapar.  
  
  
Bu konu da şimdilik bu kadar yeterli sanırım. Umarım yararlı bir yazı olmuştur. Herkese iyi çalışmalar.
  
  
Engin ÜNAL
