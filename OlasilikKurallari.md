[Ana Sayfa](https://enginunal.github.io/)

# Olasılık Kuralları


Olasılık kuralları, temel olasılık konularına giriş ve olasılık içeren olaylara yaklaşım açısından bilinmesi gereken temel kurallardır. Bu yazıda olasılık kuralları ile ilgili temel bilgiler vermeye çalışacağım. Olasılık konusu elbette derin ve matematiksel olarak detayları çok bir konudur, fakat benim üzerinde durmak istediğim özellikle giriş seviyesinde bir bakış açısı sağlamaya yardımcı olmaktır. 
Bu yazıda veya diğer yazılarımda matematiksel detaylara girip konuyu içinden çıkılamaz duruma getirmekten çok işin özünü verip merak edenleri araştırmaya yönlendirmeyi tercih ettiğimi belirtmek isterim.
Olasılık kurallarının isimlendirmelerini kolay anlaşılması amacıyla biraz farklılaştırdım, bence bu şekildeki isimlendirmeler akılda kalıcı oluyor. Kuralları kısaca özetleyip örneklerle pekiştirmeye çalışacağım. Daha net anlamak için farklı kaynakları ve tanımları incelemenizi özellikle öneririm.


### Toplama Kuralı
Aynı anda gerçekleşmeyen(olasılıkları kesişmeyen/ayrık)(mutually exclusive) olayların toplam gerçekleşme olasılığı, her olayın gerçekleşme olasılıklarının toplamına eşittir.  

<code>P(A veya B) = P(A) + P(B)</code>  

Örnek: Elimize bir zar olsun. Zarı attığımızda 2 veya 5 gelme olasılığı nedir?  

P(2) = 1/6  
P(5) = 1/6  
P(2 veya 5) = P(2) + P(5)  
P(2 veya 5) = 1/6 + 1/6 = 1/3 çıkar.  


### Ortaklı Toplama Kuralı
Olaylar birlikte de gerçekleşebiliyorsa(olasılıkları kesişiyorsa)(non-mutually exclusive) diğer ifadeyle ortak olasılık olduğu durumlar varsa kullanılır.  

<code>P(A veya B) = P(A) + P(B) - P(A ve B)</code>  

Örnek: Bir sınıfta 17 erkek ve 13 kız toplam 30 öğrenci olsun. Sınavda 4 erkek ve 5 kız tam not A aldı. Sınıftan rasgele bir öğrenci seçtiğimizde bunun kız öğrenci veya A alan öğrenci olma olasılığı nedir?  

P(Kız veya A) = P(Kız) + P(A) – P(Kız ve A)  
P(Kız veya A) = 13/30 + 9/30 – 5/30 = 17/30 sonucunu verir.  


### Bağımsız Çarpma Kuralı
Bağımsız olayların(olayın gerçekleşmesi diğerinin gerçekleşmesini etkilemiyorsa) gerçekleşme olasılığı, bu olasılıkların çarpımına eşittir.  

<code>P(A ve B) = P(A) * P(B)</code>  

Örnek: Elimizde bir bozuk para ve bir zar olsun. İkisini de aynı anda atalım. Paranın tura gelme ve zarın 3 gelme olasılığını hesaplayalım.  

P(Tura) = 1/2  
P(3) = 1/6  
P(Tura ve 3) = 1/2 * 1/6 = 1/12 buluruz.  

Örnek : Kavanozda 3 kırmızı, 5 yeşil, 2 mavi ve 6 sarı şeker bulunsun. Bir şeker çekildikten sonra kavanoza konuluyor ve ikincisi çekiliyor. Arka arkaya çekilen iki şekerin önce yeşil sonra sarı gelme olasılığı nedir?  

P(yeşil) = 5/16  
P(sarı) = 6/16  
P(yeşil ve sarı) = 5/16 * 6/16 = 30/256 bulunur.  

Örnek: Bir okul anketi, 10 öğrenciden 9'unun pizza sever olduğunu tespit etti. Rasgele seçilen üç öğrencinin de pizza sevmesi olasılığı nedir?  

P(1. Öğrenci pizzasever) = 9/10  
P(2. Öğrenci pizzasever) = 9/10  
P(3. Öğrenci pizzasever) = 9/10  
P(1. Ve 2. ve 3. Öğrenci pizzasever) = 9/10 * 9/10 * 9/10 = 729/1000 bulunur.  


### Bağımlı Çarpma Kuralı
Gerçekleşmesi beklenen olaylar bağımlı ise bu olayların ortak olasılığını hesaplamakta kullanılır.  

<code>P(A ve B) = P(A) * P(B|A)</code>  

Koşullu Olasılık : Bir olayın gerçekleştiği bilindiğinde diğerinin gerçekleşme olasılığına koşullu olasılık denir. Örneğin B bilindiğinde A olayının koşullu olasılığı : P(A|B) olarak ifade edilir.  


Örnek: Sınıfta 12 erkek ve 18 kız öğrenci var. Öğretmen sınıf listesinden rasgele iki öğrenci işaretliyor. Bu iki öğrencinin de kız olma olasılığı nedir?  

P(Kız1 ve Kız2) = P(Kız1) * P(Kız2|Kız1)  
P(Kız1 ve Kız2) = 18/30 * 17/29 = 306/870 bulunur.  

Örnek: Üretilen 20 şişeden 3’ü hatalı üretilmekte. Testlerde arka arkaya 3 numune alınıyor ve yerine konulmuyor. Test için alınan numunelerden 3’ününde hatalı olma olasılığı nedir?  

P(Hatalı1 ve Hatalı3 ve Hatalı3) = 3/20 * 2/19 * 1/18 = 6/6840 bulunur.  


### Koşullu Olasılık
Her iki olay da birbirine bağımlı ise ve birinin gerçekleşme olasılığı diğerini de etkilemekteyse önceki konuda tanımını verdiğim koşullu olasılık formulünü kullanırız.  

<code>P(B|A) = P(A ve B) / P(A)</code>  

Örnek: Bir matematik öğretmeni sınıfa iki test verdi. Sınıfın %25'i her iki testten de geçti ve sınıfın %42'si ilk testi geçti. İlk sınava girenlerin yüzde kaçı ikinci sınavı geçti?  

P(A) = 0.42  
P(A ve B) = 0.25  
P(B|A) = P(A ve B) / P(A) = 0.25 / 0.42 = 0.60 = %60 buluruz.  

Örnek: Atatürk Lisesi’nde bir öğrencinin Teknoloji ve İngilizce dersi alma ihtimali 0.087'dir. Öğrencinin Teknoloji alma ihtimali 0.68'dir. Teknoloji alan bir öğrencinin İngilizce alma ihtimali nedir?  

P(A ve B) = 0.087  
P(A) = 0.68  
P(B|A) = 0.087 / 0.68 = 0.13 = %13  

