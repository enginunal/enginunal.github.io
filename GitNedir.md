[Ana Sayfa](https://enginunal.github.io/)

# Git Nedir? Temel Komutlarla Git  


Bu yazıda, yazılımcıların kod geliştirme süreçlerinin önemli bir parçası olan versiyonlama ve kaynak kod yönetimi konularında git kullanımına ve komutlarına kısaca değineceğim.  
  

### Git

Git, Linux işletim sistemini de geliştiren Linus Torvalds tarafından 2005 yılında kullanıma sunulmuştur. O yıla kadar kullandıkları BitKeeper ile yaşanan anlaşmazlıklar sonucunda Linus Torvalds dağıtık bir versiyon ve kod kontrolü sistemi tasarımlamaya başlamış ve 2005 yılında bunu tamamlayarak topluluğa sunmuştur. İlk aşamada linux çekirdeği kodlamalarında kullanılan git daha sonra dünyada en çok kullanılan versiyon kontrol ve kaynak kod kontrolü sistemi olmuştur.  
  
Stackoverflow anket verilerine göre yazılım geliştiricilerin günlük kod checkIn istatistikleri :  

![image](/images/GitNedir/dailyCheckInStatsStackOverflow.jpg)  
  
  
Ve yazılımcıların kod yönetiminde kullandıkları araçların listesi :  

  
![image](/images/GitNedir/gitUsageStatsStackOverflow.jpg)  
  
  
Sektördeki git kullanımının ne kadar yaygın ve ciddi bir oranda olduğu yukarıdaki tablodan da ortaya çıkmaktadır. Muhtemelen bu tablo gelecek yıllarda da değişmeden devam edecektir. Yazılım hayatına yeni başlayacak arkadaşlara ve daha deneyimli fakat git tecrübesi olmayan arkadaşlara önerim bu sisteme önem vermeleri ve öğrenme listelerinde üst sıraya yazmaları olacak.  
Source Code Management, version Control Management isimleriyle de bilinen kısaca kod yönetimi olarak ta adlandırılan sistem neden bu kadar önemlidir? 
Çünkü bu kavramın doğru uygulanması bundan sonra gelecek adımların da doğru atılabilmesi açısından değerlidir. Sürekli gerçekleşmeye devam eden ve otomatize edilmiş süreçler olan Continuous Integration, Continuous Deployment, Continuous Delivery süreçlerinin gerçeklenebilmesi için ilk aşama olan CI(cont. integ.) tarafında versiyonlama, kod kalitesi, derleme, test gibi alt süreçler mevcuttur. İşte bu alt süreçlerin tasarımı, devamında gelen tüm mimarinin omurgasını oluşturacağından doğru ve güncel bilgiler ile oluşturulması oldukça önemlidir. Yazının konusu daha teknik olarak devam edeceğinden git sisteminin kurulması ve kullanılması ile devam edelim.
  
  

### Git Kulumu  

Eğer sisteminizde mevcut değilse Git kurmak için https://git-scm.com/downloads adresinden kurma işlemini gerçekleştirebilirsiniz. Yazıyı yazarken makinamda Ubuntu kurulu olduğundan Debian temelli Linux  dağıtımları için 

```
sudo apt-get install git-all 
```



### Git Repository Oluşturmak ve Dosya İşlemleri  


Kurulum işlemleri sonrasında denemelerimizi yapabilmek için ilk repository oluşturma işlemine geçelim. Bunun için bir klasör oluşturacağız.

```
mkdir repo-deneme
```

Klasörün içerisinde girip bu klasörü git repository'sine dönüştürmek için :

```
git init
```

repo-deneme klasörümüzde git init işlemini yaptık. Artık durumunu git komutuyla görebiliriz.

```
git status

On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Henüz herhangi bir ekleme/değişiklik yapılmamış boş bir repository hazırlamış olduk. Şimdi ilk dosyayı bu klasör içerisinde oluşturup repo'ya ekleyelim.

```
touch deneme.txt

git stautus


On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        deneme.txt

nothing added to commit but untracked files present (use "git add" to track)
```


git deneme.txt dosyamızı algıladı ve untracked durumunda gösterdi. git sisteminde dosyaların durumları aşağıdakilerden biri olacaktır.

| durum | açıklaması |
| --- | --- |
|untracked| Dosyanın sistemde henüz bir izi yoksa. Yeni dosya ekleme işlemlerindeki durumdur.|
|tracked| Dosyanın git tarafından tanındığı ve değişiklik algılandığı durumda.|
|unstaged| Tanınan dosya içerisinde değişiklikler var ama commit edilmesi için stage edilmemiş.|
|staged| Dosya commit edilmek için hazır. Stage edilmiş.|
|deleted| Dosya silinmiş ve git sisteminden kaldırılmalı.|


![image](/images/GitNedir/stageCommit.jpg)



untracked, staged, unstaged kavramları nedir bunları açıklamaya çalışayım. deneme.txt dosyamızı klasörde oluşturmuştuk. Dosya henüz sistemde kayıtlı olmadığından untracked durumundadır. Dosyayı sisteme kaydettiğimizde staged konumuna geçer. staged durumunda olan dosya commit işlemi yapılmazsa değişiklikler sisteme aktarılmamış olur. staged konumu değişikliklerin aktarılması için ön adımdır. Dosya içerisinde herhangi bir editleme yaptığımızda unstaged durumuna geçer. Değişiklikler sonrasında unstaged durumundan staged durumuna alınması gerekir ki sonraki aşama olan tracked durumuna alınabilsin. Bu yazdığımız komutlarla yapmak istersek şu şekilde olacaktır.

git add deneme.txt  ile dosyayı staged konumuna aldık. git status ile baktığımızda modified: deneme.txt mesajı commit dosyanın stage edildiğini fakat commit edilmediğini anlatır.
git commit -m "dosya ekleme mesaji"  staged konumundaki değişikliklerin commit edilmesi için kullanılır. 

Şimdi dosya içerisinde değişiklik yapalım, içerisinde herhangi bir yazı ekleyip kaydedelim. commit edilmiş bir dosya üzerinde değişiklik yaptığımızda unstaged durumuna düşer ve commit edilebilmesi için tekrar staged durumuna almamız gerekir.

git add deneme.txt ile staged konumuna aldık.
git commit -m "dosya icerisinde degisiklik" komutu ile commit ettik.

Bu işlemleri yaparken git status ile o anki durumu inceleyebilirsiniz. Veya şu ana kadar yaptıklarınızı görmek için git log komutunu kullanarak inceleyebilirsiniz. Şimdiye kadar anlattıklarımla bir git repository oluşturduk, buna yeni bir dosya ekledik ve bu dosya üzerinde değişiklik yaparak değişiklikleri commit ettik. Şimdi çoklu çalışma ortamlarında birden çok yazılımcının aynı kod üzerinde nasıl çalıştığını inceleyeceğiz.



### Git Branch İşlemleri


Branch, bir ana kod ekseninde birden çok yazılımcının çalışabilmesine olanak sağlar. Kavram olarak branch bir ağaç gövdesinden ayrılan dalları simgeler. 


![image](/images/GitNedir/branches.jpg)


Ana dal master olarak isimlendirilir. Eğer master üzerinde değil de kendimize ait bir alanda kod üzerinde değişiklik yapmak istiyorsak yeni bir branch açarak başlarız. Açtığımız bu yeni branch, master'ın kopyasıdır farkı ise bizim bundan sonra yapacağımız değişikliklerin sadece kendimize ait olan branch üzerinde yapılacak olması ve master'ı etkilememesidir. Branch üzerindeki işimiz bittiğinde ve master'a bu değişikliklerin aktarılmasına karar verdiğimizde master'a bunları commit ederiz ve branch ile işimiz bittiği için artık silebiliriz. Temel olarak branch ile çalışma prensibi bu şekildedir. Çoklu çalışma yürütülen projelerde master üzerinde bir değişikliğin yapılmasını belli kurallara bağlamak, master branch'in herkes tarafından değiştirilmesinin yaratacağı karmaşayı önlemek ve otomatize işlemlerin sağlanabilmesi için kurulacak mimarilerin tasarımı açısından branch yaygın bir kullanımdır. Şimdi master branch haricinde bir branch oluşturup üzerinde kod değişikliklerimiz gerçekleştirecek ve bunu master branch'e commit ederek süreci sonlandıracağız.


git checkout -b branch-denemesi

Komutu ile branch-denemesi isminde yeni bir branch oluşturuyoruz. git branch komutu ile branch listemizi ve hangi branch üzerinde olduğumuzu görebiliriz. Komut sonucunda * ile işaretli olan şu anda çalıştığımız branch'i gösterir.

```
git branch
* branch-denemesi
  master
```

repo-deneme klasöründe merhaba.txt isimli dosya oluşturup bunu repository'e ekleyeceğiz, 

```
git add merhaba.txt
git commit -m "yeni dosya merhaba.txt"
```

Dosya ekleme işlemi branch-denemesi harici diğer master branch için aktif olmayacaktır, yani git checkout master yaparak master branch aktif edilirse ve ls veya dir komutuyla klasör listelendiğinde merhaba.txt dosyası olmayacaktır. Tekrar git checkout branch-denemesi yapılarak yeni açtığımız branch aktif edildiğinde dosyanın klasörde olduğunu görebilirsiniz. İşte bu mimari sayesinde master üzerinde değişiklik yapmadan tüm işlemleri açacağımız yeni branch içerisinde yapıp son aşamada bunları master branch'e gönderebiliriz ve biz gönderene kadar master bizim branch'imizle ilgili hiçbir değişiklikten etkilenmez. Branch içerisinde yapılan değişikliklerin master üzerine gönderilmesi işlemine merging denir. git merge komutu ile bu değişiklikler master üzerine gönderilir. Şimdi git checkout master ile master branch'i aktif edelim ve merge edilmeyen hangi branch var listeleyelim.


git branch --no-merged

branch-denemesi merge edilmemiş. Bunu merge edip süreci tamamlamak için merge komutu kullnılır ardından işimizin bittiği branch-denemesi isimli branch'i silelim.

git merge --no-ff branch-denemesi -m "yeni dosya eklendi"

git branch -D branch-denemesi


Bu konuda yeni bir branch açtık ve bunun içerisinde bir dosya oluşturup daha sonra yaptığımız değişiklikleri master üzerinde merge ettik ve açtığımız branch'i sildik ve sürecimizi tamamladık. Şimdiye kadar anlattıklarımla git üzerinde bir repository oluşturup temel komutlarla çalışabilir ve branch kullanabilir noktaya geldik. Konunun devamında lokalde olmayan yani uzak repository kavramından bahsedeceğim. Git repo'larımız uzak bir sunucu üzerinde bir servisle hizmet veriyor olabilir(GitHub gibi) ve bir çok yazılımcı tarafından kullanılıyor olabilir. Bu sunucularındaki kodlar üzerindeki değişiklikler ve işlemlerin yönetilmesi nasıl gerçekleşiyor ve hangi komutlarla yapılıyor biraz da bu konuya değineceğim.



### Remote Repository


Remote repo veya uzak depo bir kod kontrolü yönetim sunucusu üzerinde bulunan repo'lar için kullanılan genel bir isimdir. Bu şekilde farklı konumlardaki yazılımcıların ortak bir repository üzerinde senkronize çalışabilmesi mümkün olmaktadır. Remote repo sunucularına bağlanan yazılımcılar burada kendi projelerine ait repo'yu lokal makinalarına indirir(clone) ve çalışmalarını tamamladığında veya belli periyotlarla remote repo'ya gönderir(push). En bilinen remote repo sunucusuna örnek GitHub verilebilir. Kısaca bu işlemlerin komutlarını inceleyelim.


![image](/images/GitNedir/git-local-remote.jpg)


Bir remote repo üzerindeki kodu clone'lamak için git clone [URL] komutu kullanılır [URL] ile verilen repo linkindeki proje lokale git tarafından indirilir ve çalışmaya hazır hale gelir. Lokal repo üzerinde staging ve commit işlemleri için önceki konuda verdiğim komutlar kullanılmaktadır. Lokaldeki işlerin remote repo'ya gönderilmesi için git push komutu kullanılır. Server üzerindeki kodda sizdekinden daha güncel değişiklikler mevcutsa bunları alabilmek için öncelikle git fetch komutu ile değişikliklerin listesi alınır ve ardından git pull komutu ile değişiklikler indirilir.

Yazıyı burada kesip sonraki yazımda Gitlub ve Jenkins kurulumlarını yapıp konfigürasyonlarıyla ilgili temel bilgiler vereceğim.

Teşekkürler.



Engin Ünal




