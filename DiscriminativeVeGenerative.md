# Discriminative ve Generative Modeller


Supervised learning altındaki classification işlemlerinde Discriminative ve Generative modeller hakkında kısa bilgi vermeye çalışacağım. 
Aslında kelimelerin anlamlarından gitsek bile farkın ne olduğunu kestirmemiz mümkün. Discriminative kelimesini ayrım yapan/fark gözeten, Generative kelimesini ise üretebilir/yaratabilir olarak anlamlandırabiliriz. Bu durumda Discriminative model verideki farklara bakan ve buna göre farklılık arasına bir sınır koyup(desicion boundary) bu şekilde sınıflandıran, Generative model ise veri farklılıklarını modelleyip/anlayıp gruplayan ve sınıflandırmayı grupladığı bu model üzerinden yapan algoritmadır diyebiliriz.


Örneğin logistic regression bir Discriminative öğrenme algoritmasdır. Bu nasıl çalışır? En basit anlatımla A ve B etiketine sahip iki veri setimiz olsun. A ve B olarak sınıflandırdığımız veri setinin ayrımını yapmak için A etiketi ve B etiketi verilerinin arasından düz bir hat geçirir buna desicion boundary denir. Bu hattın bir tarafı A diğer tarafı B olarak ayrılır. 
Desicion boundary’i doğru bulabilmek için gradient descent kullanılır, hattın minimum hatayla çizilmesi gradient descent algoritması ile mümkündir. Gradient descent algoritması ile hata eğrisinde düze yakın bir noktaya ulaşmayı yani desicion boundary çizgimizin en optimum noktadan geçmesini sağlarız. Bu şekilde optimum bir hat çizerek A ve B olarak sınıflandırdığımız verileri modellemiş oluruz. 
Yeni gelen verinin A veya B olarak ayrımını yapabilmek için bu şekilde bir model elimizde olmalıdır. Modele verdiğimiz yeni verinin A veya B sınıfına girip girmediği tahmini bundan sonra yapılır. Discriminative öğrenme algoritması desicion boundary’e bakar ve tahmin edilmesi gereken veri hangi tarafta kalıyorsa tahmini o yönde yapar.


Generative modelde elimizdeki A ve B olarak etiketlenmiş veriyi algoritma alır, A ve B etiketinin özelliklerini, A ve B olmasının nedenlerini öğrenir. Buna göre yeni gelen tahmin edilmesi gereken veriyi buna göre A veya B olarak sınıflandırır. 
Yani algoritma A ve B etiketlerini modeller, bu modeli yeni gelen verinin neye uyduğunun tahmin edilmesinde kullanır.
