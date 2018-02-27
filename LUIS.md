[Ana Sayfa](https://enginunal.github.io/)


# LUIS - The Language Understanding Intelligence Service


LUIS, Microsoft tarafından geliştirilmiş bir yapay zeka servisidir. Natural Language Processing (NLP) kullanarak verilen cümleleri yorumlar, ayrıştırır ve hangi amaca yönelik olduğunu sınıflandırarak döner. LUIS ile uygulamalar arasındaki veri alış verişi HTTP endpoint aracılığı ile olmaktadır.

Bir LUIS uygulamasını dizayn ederken temel üç kavramın bilinmesi önemlidir. Bunlar:

#### Utterance
İfade. Kullanıcıdan gelen ve yorumlanması gereken metin girişi. "Ankara'ya bilet alacağım" veya "Rezervasyon" veya Ankara uçuşu" gibi bir ifade olabilir.

#### Intent
Amaç. Kullanıcının gerçekleştirmek istediği işlemleri temsil eder. Kullanıcının cümlesindeki hedeftir; örneğin, bir fatura ödemesi veya bir haber makalesini bulma gibi.

#### Entity
Varlık. Kullanıcının amacıyla alakalı bir sınıfı temsil eder. “Ankara'ya bilet alacağım" sözcüğünde, "Ankara", konum türü bir varlıktır.




Şimdi bir LUIS uygulamasının nasıl oluşturulacağını açıklamaya çalışacağım.


## LUIS Uygulamasının Oluşturulması


Azure portal(portal.azure.com) sitesine girip Cognitive Service altındaki Language Understanding Intelligent Service seçeneğinden bir LUIS uygulaması yaratılır.



![image](/images/Luis/1_CreateAzureLUISApp.jpg)




Daha sonra yine aynı microsoft hesabıyla LUIS’in kendi sitesine(luis.ai) girilip sign in edilir. My Apps kısmından New App ile yeni bir uygulama oluşturulur. Ben bu yazıyı yazdığım sırada 10 dil desteği vardı ve bunlar arasında Türkçe mevcut değildi. Bu nedenle denemelerimi İngilizce yaptım.




![image](/images/Luis/1_CreateLuisApp.jpg)






Uygulamamızı oluşturduktan sonra dashboard görüntüsü aşağıdaki gibi olacaktır.


![image](/images/Luis/2_CreatedAppOverview.jpg)






Artık uygulamamıza Intent, Entity, Utterance tanımlamalarımızı yapabiliriz. Öncelikle intent ekleyerek başlayalım. Intent sayfasında Add Intent ile yeni intent ekleriz.


![image](/images/Luis/3_CreateIntent.jpg)





Intent eklemesini yaptıktan sonra Utterances ekranı gelir, bu ekrandan close door intent’inin hangi cümlelerden yorumlanacağı tanımı yapılır.Yani utterances sayfasına girdiğim cümleler close door intent’inin kast edildiği cümleler olmalıdır.



![image](/images/Luis/4_CreateUtterance.jpg)






Bu cümlede door kelimesi bizim entity değerimiz olacak. Door kelimesi üzerine gelip create entity işlemi ile entity oluşturabiliriz.





![image](/images/Luis/4_CreateEntity.jpg)





Aynı şekilde open door intent’i tanımlayıp utterance kısmına “please open the door” cümlesini tanımlayıp devamında bu cümledeki entity olan door kelimesini entity olarak tanımlarız.

Daha sonra Train & Test kısmından Train Application yaparak uygulamamızı eğitiriz. Bu ekranda interactive test kısmından uygulamamızı test edebiliriz. Test kısmında yazdığımız cümleler yorumlanır ve ilgili intent ile ilişkilendirilip bir tahmin yüzdesi verilerek ekrana yazar.




![image](/images/Luis/5_TestApp.jpg)







Bu ekrandan kapıyı aç veya kapıyı kapat intent’leriyle ilgili farklı cümleler kurabilir ve bunların model tarafından hangi oranda doğrulukla anlaşıldığını ve ilgili intent ile ilişkilendirildiğini görebilirsiniz.

Modelin testi de tamamlandıktan sonra publish edilme aşamasına geçilir. Publish App sayfasından geliştirdiğimiz uygulamamız bir web servis olarak publish edilebilir. Publish işleminde bize bir Endpoint Url verilir. Publish edilen uygulamamıza bu url ile erişebilir.


Publish edilen serivsimize erişim(consume) için c#, python gibi güncel diller kullanılabilir. Bununla ilgili örnekler azure portalde luis altındaki quick start sayfasında mevcut. Ben bu servise C# Consol Application ile nasıl erişildiğinin örneğini github hesabıma yükledim. Aşağıdaki adresten ulaşabilirsiniz.



(https://github.com/enginunal/ConsumeLuisConsoleApp)



Bu yazıda LUIS uygulamasının nasıl oluşturulduğunu, içindeki kavramların neler olduğunu ve ne işe yaradığını, üretilen yapay zeka modelinin dış dünyaya nasıl açıldığını ve sonrasında nasıl erişildiğini özetlemeye çalıştım. Umarım yararlı olmuştur.



İyi günler.
