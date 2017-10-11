[Ana Sayfa](https://enginunal.github.io/)


# Yapay Zeka Öğrenme Teknikleri - Giriş


## Supervised Learning

Denetimli Öğrenme olarak ta dilimize çevrilebilir. Seçeceğimiz öğrenme algoritmamıza modelleme yapabileceği yeterlilikte verinin ve bu veriden ulaşılmaya çalışılan sonucun verilmesi gerekir. Algoritmamız eldeki veriyi ve bu verinin sonucunu kullanarak bir model geliştirir. Geliştirilen bu modelin geçerliliğini ve hata oranlarını bilebilmek için elimizdeki veri ve sonuçları ile sınarız.
Eldeki hazır veri seti kullanılarak geliştirilmiş ve sonrasında test verisi ile geçerliliği sınanmış modelimizin yeni gelecek veriden doğru tahmini sonuç çıkarması bazı kriterlere bağlıdır. Doğru modelleme yapılmamışsa çıkacak sonuçlar da gerçek durumdan uzak olacaktır. Dikkat edilmesi gereken kriterler öğrenme algoritması seçimi, verinin gerçek durumu ne kadar yansıttığı, test verisinin ne kadar doğru seçildiği ve hazırlandığı(bu konu çok önemli ve uzun bir konudur) gibi.

### Regression

Sayısal giriş değerleri ile sayısal ve süreklilik içeren bir çıkış değeri öngörmemiz gerektiğinde kullanılır. Modeldeki hata hesaplanmasında RMSE(Root Mean Squared Error) ve MAE(Mean Absolute Error) gibi hata hesaplama yöntemleri kullanılır. Hata sonuçlarının birim olarak değil de relatif olarak alınması için de RAE(Relative Absolute Error) ve RSE(Relative Squared Error) kullanılır.
Hata sonucu ne kadar düşükse model o kadar başarılı olmuş demektir.

### Classification

Eldeki verinin sınıflandırılması veya kategorize edilmesi amacıyla kullanılır. Sık kullanılan Classification algoritmaları:


* Logistic Regression
* Desicion Trees / Classification Trees
* AdaBoost
* SVM(Support Vector Machines)
* Random Forests
* Neural Networks


Örneğin elimizdeki verinin bir kısmını A etiketiyle diğerini B etiketiyle etiketlemiş olalım. Sınıflandırma algoritması bu verileri alır, çalışır ve bunlardan bir model oluşturur. Oluşturulan model A ve B etiketlerinin nasıl ayrılacağını öngören bir modeldir. A ve B etiketli verileri birbirinden ayıracak bir yol bulur ve bu yola decision boundary yani karar sınırı denir. Sınırın bir tarafı A etiketli veri diğer tarafı B etiketli veri olacak şekilde model üretilir. Sonrasında modelimize henüz etiketlenmemiş ve hangi etikete ait olduğunu tahmin etmesini istediğimiz veriyi gönderdiğimizde bunun A veya B etiketinin hangisine uyduğunun tahmini yapar ve etiketler. 

Binary classification algoritmasını ele alırsak, bu model ile eldeki veriler 1 ya da 0 olarak sınıflandırır ve bu iki durumdan hangisine uyduğunu belirleyebiliriz. 1 ya da 0 olma kararı bir eşik(threshold) yardımıyla alınır. Eşik değerinden düşük olan veriler 0, eşik değerinden büyükler ise 1 olarak sınıflandırılır.
Supervised learning tekniğinde modelin öngörüleri eldeki verilerle test edilir ve modelin geçerliliği ve performansı sınanmış olur. Binary Classification modelinin tahminleri test verisi ile kıyaslandığında:


Model 1 olarak tahmin etmiş ve test verisi 1 ise : Doğru Pozitif (True Positive)(TP)

Model 0 olarak tahmin etmiş ve test verisi 0 ise : Doğru Negatif (True Negative)(TN)

Model 1 olarak tahmin etmiş ve test verisi 0 ise : Yanlış Pozitif (False Positive)(FP)

Model 0 olarak tahmin etmiş ve test verisi 1 ise : Yanlış Negatif (False Negative)(FN)



Elde edilen bu TP,TN,FP,FN sayıları ile Confusion Matrix ismi verilen bir matriks oluşturulur ve sınıflandırma modelimizin performansının hesaplanmasında kullanılacaktır. Confusion Matrix veya Contingency Table da denilmektedir, amacı olasılıkların bir tabloda gösterilmesidir.

Örnek Confusion Matrix:

![Image](https://1.bp.blogspot.com/-UYkYLsH5xxw/WdIna1UNUcI/AAAAAAAAAXc/eyNxA_xbmgMHeNYAlCmNNmclAcZhFGM6gCK4BGAYYCw/s320/confusionmatrix.jpg)


Confusion matrix kullanılarak hesaplanan performans ölçümleri şunlardır:


**Accuracy** : Doğruluk. İsabetli tahmin edilen sınıflandırmaların, toplam sınıflandırılma sayısına bölümü.

Accuracy = (TP + TN) / ( TP + FP + TN + FN)


**Presicion** : Hassasiyet. Sınıflandırıcıdan olumlu bir tahmin alındığında, bunun gerçekte ne kadar doğru olduğunu belirlemede kullanılır. Bu da doğru tahmin edilen pozitif öngörüler sayısı ile doğru veya yanlış toplam tahmin edilen pozitif öngörülerin sayısına bölünür.

Presicion = TP / (TP + FP)


**Recall** : Çağırma. Diğer adıyla Duyarlılık veya TPR(True Positive Rate)(Gerçek Olumlu Oran). Sınıflandırıcının yaptığı olumlu tahminlerin hangi kısmı kesin olarak doğru bu durumu bulmak için kullanılır. Bir başka deyişle, olumlu tahminlerin sayısının, test verilerindeki pozitif sınıflandırılan değer sayısına bölünmesidir.

Recall = TP / (TP + FN)



Recall daha önce de belirttiğim gibi True Positive Rate ismiyle de geçer, bunun yanında benzer bir oranlama hesabı daha vardır o da False Positive Rate. FPR ise olumsuz tahminlerin oran hesaplanmasında kullanılır. TPR ve FPR ikisi ROC(Receiver Operating Characteristic) eğrisi denilen bir eğirinin çizilmesinde kullanılır.TPR ve FPR formülleri:

TPR = TP / (TP + FN)
FPR  = FP / (FP + TN)


Örnek ROC Eğrisi:

![Image](https://1.bp.blogspot.com/-9wWWogTvjyQ/WdInvOLgCuI/AAAAAAAAAXk/ofFmNikdQ6woQkweSZPj8BueAIPAzjWPgCK4BGAYYCw/s1600/ROCEgrisi.jpg)


ROC eğrisinin altında kalan alana ise AUC(Area Under The ROC) denir. Eğri altındaki alan veya AUC, modelin ne kadar iyi öngöreceğini gösteren bir göstergedir. Genellikle, AUC alanı ne kadar geniş ise o kadar iyidir. Grafiğin sol üst köşesine mümkün olduğunca yakın olunmak istenir.



## Unsupervised Learning


Supervised Learning tekniğindeki gibi modelimizi geliştirmek ve eğitmek için elimizdeki veri sonuçlar içermeyebilir, etiketlenmemiş veya kategorize edilmemiş olabilir. Yani sadece veri kümesine sahip olabiliriz ve bu veriler herhangi bir sonuçla ilişkili olmayabilir. Bu durumlarda veri içindeki benzerlikleri keşfedip gruplamak için bir takım algoritmalar kullanılır. Bunlar verideki benzerlikleri gözlemleyerek veriyi kümelere ayırır ve onları gruplar. Amaca ve veriye göre farklı algoritmalar (K-Means , DBSCAN, Gaussian Mixture Model, ..) kullanılmaktadır.


### Clustering

Kümeleme, bir veri içindeki benzerlikleri gruplamak için kullanılan bir tekniktir. Kümeleme işlemini yapan algoritmalardan en popüler olanı K-Means clustering algoritmasıdır.

##### K-Means Algoritması :
İteratif bir algoritmadır, yani ideal sonuca ulaşana kadar çalışmaya(kümeleme işlemine) devam eder. Elimizdeki veri uygun özelliklere sahip ise bu veriden istenen sayıda kümeleme çıkarmakta kullanılır. Oluşturulacak küme sayısı K ile ifade edilir. K kümelerinin merkezinde Centroid ismi verilen küme merkez noktası bulunur.
Algoritma önce rastgele centroid atar ve devamında bu centroid’e yakın olan noktaları küme içine alır. Küme içinde kalan noktaların küme merkezine ortalama uzaklığı ve küme merkezinin diğer küme merkezlerine olan ortalama uzaklığı gibi hesaplamalar yapılıp iteratif olarak küme merkezi değiştirilir. Yeni atanan küme merkezine en yakın noktalardan tekrar bir küme oluşturulur ve işlem bu şekilde mevcut küme merkezi değişmeyene dek (ideal konuma ulaşana kadar) kaydırılır.


##### Principal Component Analysis(PCA) :
PCA, ismine bakıldığında ve internetteki kaynaklar incelendiğinde mantığının zor gibi gözükmesine rağmen öyle değil. Hem anlaşılabilir hem de bir cümleye sığdırarak anlatmaya çalışacağım.

PCA temel olarak elimizdeki verinin boyutlarını indirgemeye yarar, bu şekilde kümeleme işlemimizi daha az boyut kullanarak ve karmaşası azalmış bir şekilde çözmemize yardımcı olur.

Yukarıdaki cümle yeterli olmadıysa pek çok sitedeki karmaşık anlatımla verildiğinde şöyle anlatılabilir. Elimizde N boyutlu veri olsun, öncelikle bunun NxN boyutlu kovaryans Matrisi bulunur, matrisin N adet eigen value değerleri bulunur, bunlardan eigen vector’ler hesaplanır. Verimiz bu eigen vector’lere iz düşürülerek boyut indirgenmiş olur.

Tekrar anlaşılabilir versiyona geçildiğinde iki örnekle bitireyim. Örneğin elimizde iki boyutlu verimiz olsun, PCA ile bu verileri bir boyuttaki vektöre indirgeyebiliriz. Ya da üç boyutlu verimiz var diyelim. Boyutları x1,x2,x3 olsun. Bu veriyi 2 boyutlu bir yüzeye indirgeyebiliriz(elimizde iki vektör olur). Temel olarak PCA ile elimizdeki verinin bir boyut aşağıya indirgemesini yapabiliriz.

