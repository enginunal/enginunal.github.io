[Ana Sayfa](https://enginunal.github.io/)


# Custom Vision AI


Microsoft’un kullanıma sunduğu görsel tanıma ve sınıflandırma yapay zeka servisidir. Daha önce LUIS konusunda da anlattığım gibi kullanması kolay, herhangi bir kodlama gerekmeden bir modelin üretilip publish edilebileceği ve çağrılabileceği bir yapıdır.
Kullanımı en basit servis diyebilirim, sadece görselleri yükleyip modeli train ettikten sonra sınıflandırma denemelerini yapabilirsiniz.

Öncelikle [customvision.ai](https://customvision.ai/) sitesinden microsoft hesabınızla giriş yapıyorsunuz. Sonrasında yeni proje yaratılıyor.


![image](/images/CustomVisionAI/1.jpg)



Proje yaratıldıktan sonra görseller yükleniyor. Görsel yükleme ekranında yüklenen görsellere tag veriliyor. Bu tag’leme işlemi yüklenen görsel setinin hangi sınıflandırmaya ait olduğunu belirtmek için gerekli.


![image](/images/CustomVisionAI/2.jpg)



Ben örnek olarak qashqai ve auris fotolarını yükledim ve auris fotolarına toyota ve auris etiketini verdim. Qashqai fotolarına ise nissan ve qashqai etiketini verdim.
Daha sonra yüklenen bu resimler train ediliyor.


![image](/images/CustomVisionAI/3.jpg)



Modelimizi train ettikten sonra denemelerimizi yapabiliriz.
Önce modelimizde olmayan bir qashqai resmini vererek test edelim ve modelin bu resmi hangi olasılıkla hangi marka ve modelden biri olduğunun tahminini görelim.


![image](/images/CustomVisionAI/4.jpg)



Evet %99 üstünde tahminle Nissan Qashqai olarak sonucu aldık. Şimdi de auris görselini deneyelim.


![image](/images/CustomVisionAI/5.jpg)



Bu tahminde de önemli bir başarı var, her ne kadar nissan tahmini de yüksek gelse de yine de iyi. Modelin tahminlerini geliştirme başarısı tamamen yüklenen  görsel sayısı ve bu görsellerin niteliği ile doğru orantılı artacaktır.

Ayrıca tahminlerde yanılmaların modele bildirilmesi ve düzeltilmesi imkanı da var. Bunun için predictions sayfasından daha önce tahmini yapılan ve modelin tahminde saptığı görselleri seçip tekrar tag'leme işlemi yapılabilir ve bu resimler de model eğitimine eklenebilir.

Beş dakikada kolayca bir yapay zeka servisi geliştirmenize olanak sağlayabilmesi ve pratik olması bence bu işe yeni başlayanlar için gayet cesaretlendirici olmuş. 



İyi günler.
