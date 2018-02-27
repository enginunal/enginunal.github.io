[Ana Sayfa](https://enginunal.github.io/)

# Azure Functions İle HttpTrigger Örneği

Serverless computing, kodun altında çalışan framework + işletim sistemi + sunucu gibi konulara odaklanmak ve bunların bakım ve 
performans yönetimleriyle uğraşmak yerine sadece yapılan işe odaklı bir yapı sunmasıyla oldukça popüler konulardan biri haline geldi.  
Benim düşünceme göre gün geçtikçe farklı serverless yapılarının desteklediği dil ve framework çeşitliliği arttıkça
genel kullanımın bu alana doğru ilerleyeceği yönünde.   
Mutlaka geçiş sürecinde birtakım zorluklar olacaktır fakat kullandığın kadar öde sistemi ve altyapı yatırımına gerek 
duyulmayan bu mimariler önümüzdeki yıllarda daha geniş alanlarda kullanılacaktır.  
Cloud computing konusu altında FAAS ve serverless konuları ile ilgili web üzerinde bir çok yazı ve eleştiri bulunabilir.  

Bu yazıyı spesifik olarak bir Azure Functions uygulamasının nasıl oluşturulduğu konusunda fikir vermek için yazmaya karar verdim 
umarım bu konularda merakı olanlar için faydalı olur.  
Öncelikle yazıdaki adımların uygulanabilmesi için azure hesabınızın olması gerekiyor.   
Bunun için daha önceden bir hesabınız yoksa [https://portal.azure.com](https://portal.azure.com) adresinden deneme süresi boyunca kullanabileceğiniz bir 
hesap açabilirsiniz. Hesap adımını halletiysek adım adım ilerleyerek başlayalım.  

## 1- Portal Üzerinden Azure Function App Oluşturulması

Azure portaline girdikten sonra azure functions oluşturmak için sol üst köşedeki + New ile Azure Marketplace içinden 
Compute altındaki Function App menüsüne giriyoruz.  

![image](/images/AzureFunctions1/Screenshot_1.jpg)    


Bu ekrandan App name ile uygulamamıza isim veriyoruz, varsa mevut bir resource group yoksa new ile yeni yaratıp Create ile devam ediyoruz.  

![image](/images/AzureFunctions1/Screenshot_2.jpg)  

Oluşturma işlemi sonlandığında aşağıdaki gibi mesaj gösterecektir. Go to resource ile fonksiyon ekranına gidiyoruz.  

![image](/images/AzureFunctions1/Screenshot_3.jpg)  

İsmini portalfunctest verdiğimiz uygulamamızın ekranında Functions üzerine gelerek + ‘ya tıkladığımızda yeni fonksiyon yaratma ekranı gelecektir. Bu adımda sağdaki ekrandan alttaki Custom Function’a tıklayarak devam ediyoruz. Custom olarak değil ön tanımlı senaryoları da kullanarak devam edebilirsiniz ben bu örnekte custom üzerinden gideceğim.  

![image](/images/AzureFunctions1/Screenshot_4.jpg)  

Gelen şablonlar arasından HTTP trigger şablonunu ve dil olarak C# seçimi yapıyoruz.   

![image](/images/AzureFunctions1/Screenshot_5.jpg)

Devamında trigger tanım ekranından trigger ismi veriyoruz. Benim örneğimde bu isim IsmeMesaj olarak verildi. Create ile işleme devam edip fonksiyon yaratma işleminin sonuna geliyoruz.  

![image](/images/AzureFunctions1/Screenshot_6.jpg)  

Karşımızda aşağıdaki gibi bir ekran çıkacaktır. Burada csx dosyasının içerisinde fonksiyonda ne yapılması isteniyorsa eklenebilir.  

![image](/images/AzureFunctions1/Screenshot_7.jpg)

Vereceğim örnek üzerinden devam etmek isteyenler aşağıda yazdığım kodu bu ekrana kopyalayabilir.  
Sonrasında save ile kaydedip soldaki test menüsünden test işlemlerini gerçekleştiriyoruz. Bu kod örneğinde gelen isteğin GET veya POST olmasına göre ayrı metodlar çağrılmakta ve bu metodlarda işlemler yapılmakta.  

```
using System.Net;  

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)  
{  
    log.Info("C# HTTP trigger fonksiyonuna istek geldi.");  
    string result;  

    switch (req.Method.Method)  
    {  
        case "GET":  
            result = GetMethodSample(req.GetQueryNameValuePairs());  
            break;  
        case "POST":  
            result = PostMethodSample(await req.Content.ReadAsAsync<object>());  
            break;  
        default:  
            //zaten HttpTrigger attribute'unda geet ve post tanımı yapıldığı için buraya düşmeyecektir.   
            return req.CreateResponse(HttpStatusCode.NotImplemented, new  
            {  
                durum = "sorun var",  
                mesaj = "Sadece get ve post metodları desteklenmekte."  
            });  
    }  

    return result == null  
        ? req.CreateResponse(HttpStatusCode.BadRequest, new  
        {  
            durum = "sorun var",  
            mesaj = "ad girilmesi gerekmektedir. Düzeltip tekrar deneyin."  
        })  
        : req.CreateResponse(HttpStatusCode.OK, new  
        {  
            durum = "Tamam",  
            mesaj = "Merhaba, " + result + " test fonksiyonuna hoş geldiniz."  
        });  
}  

private static string PostMethodSample(object contentVal)  
{
    return ((dynamic)contentVal)?.ad;
}

private static string GetMethodSample(IEnumerable<KeyValuePair<string, string>> valuePairs)  
{
    return valuePairs.FirstOrDefault(q => String.Compare(q.Key, "ad", true) == 0).Value;  
}

```

Kodlama sonrasında soldaki menüden Integrate ekranına geçerek trigger’ımızın hangi HTTP metodlarına izin vereceğini tanımlıyoruz.  


![image](/images/AzureFunctions1/Screenshot_8.jpg)  

Ve IsmeMesaj fonksiyonumuza tıklayarak kodlama ve test ekranına gelip test işlemini yapabiliriz.  

![image](/images/AzureFunctions1/Screenshot_9.jpg)  

Artık Azure Functions uygulamamız hazır. Bu uygulamayı test değil dışarıdan kullanmak istediğimizde ise sağ üstteki “Get Function URL” ile gerçek ortamdaki url bilgisini alabilir ve erişebiliriz.  
Geliştirdiğimiz fonksiyon için url bilgisi:  

![image](/images/AzureFunctions1/Screenshot_11.jpg)  

Ve bunu Postman uygulamasıyla denediğimizde çıktısı ise aşağıdaki gibi olmaktadır.  

![image](/images/AzureFunctions1/Screenshot_10.jpg)  

Geliştirdiğimiz bu fonksiyon uygulamasının OpenAPI tanımlamalarını da yapabiliriz. OpenAPI ile ilgili bu yazıda bir detay bulunmamakta.   
Kısaca tanımlamak gerekirse. OpenAPI Spesifikasyonu (OAS), bir hizmetin kaynak koduna, ek dokümantasyona veya ağ trafiğinin incelenmesine gerek duymadan yeteneklerinin ve özelliklerinin anlaşılmasına olanak tanıyan bir standart sunmaktadır. Şimdilik projemize nasıl eklendiği ile ilgili bilgi verip konuyu sonlandıracağım.
portalfunctiontest ekranına gelip Platform features ve buradaki API definition ekranından,  

![image](/images/AzureFunctions1/Screenshot_12.jpg)  

Açılan ekranda API definition source altındaki Function düğmesiyle OpenAPI tanım ekranı açılır.  

![image](/images/AzureFunctions1/Screenshot_13.jpg)  

Bu ekrandan Generate API definition template ile api tanımı, şablondan ürettirilir. Bu işlem sonrasında azure functions.json isminde openAPI tanım dosyası oluşturur.   
Oluşturulan tanım dosyası swagger gibi OpenAPI editörleri ile düzenlenebilir.  
  
  
  
  
## 2- Visual Studio 2017 Üzerinden Azure Function App Oluşturulması ve Publish işlemi

Eğer yüklü değilse Azure development workload yüklenmeli. Bunun için Visual Studio Tools altındaki Get Tools and Features ile modify ekranını açıp workloads sayfasından yükleyebilirsiniz.  
  
  
Yükleme işlemi sonrasında aynen diğer projeleri başlattığımız gibi yeni bir proje başlatıp buradan Azure Functions seçiyor ve isimlendirip devam ediyoruz.  
  
  
![image](/image/AzureFunctionsVS/Screenshot_1.jpg)    

Projemiz Http trigger örneği olacağından Http trigger seçip storage account olarak emulator verip devam ediyoruz.  
  
  
![image](/image/AzureFunctionsVS/Screenshot_2.jpg)    

 Karşımıza örnek code geliyor ve aşağıdaki ile değiştiriyoruz.  
   
   
![image](/image/AzureFunctionsVS/Screenshot_3.jpg)    
  
  
Yukarıdaki kodu içeren projeyi repository'lerim altına ekledim [link](https://github.com/enginunal/FunctionAppEngin) inceleyebilirsiniz.  
  
  
Bu işlemden sonra debug yapabilecek noktaya geldik ve F5 ile debug işlemini başlattığımızda Azure Functions Core Tools (cli) ile servisi başlatıp debug işlemine geçiyoruz. Eğer cli yüklü değilse bunu yüklemeyi soruyor ve evet derseniz tüm işlemleri tamamlayıp debug için hazır hale getiriyor.
  
  
![image](/image/AzureFunctionsVS/Screenshot_4.jpg)   

Bu aşamada fonksiyonumuzu, Postman gibi HTTP metodlarını kullanabildiğimiz araçlardan biriyle çağırabiliriz. Aşağıda gönderdiğim get ve post ekran çıktıları ve işlem sonuçları görülebilir.  
  
  
![image](/image/AzureFunctionsVS/Screenshot_5.jpg)   
  
  
![image](/image/AzureFunctionsVS/Screenshot_6.jpg)   
  
  
![image](/image/AzureFunctionsVS/Screenshot_7.jpg)   

Son olarak yazdığımız fonksiyon eğer publish edilecekse Publish adımından nereye publish edileceğini seçebiliriz. Ben doğrudan Azure üzerine ve yeni bir fonksiyon olarak publish edeceğim.  
  
  
![image](/image/AzureFunctionsVS/Screenshot_8.jpg)   

Eğer login olmuşsak ve azure üzerinde functions için hakkımız varsa ekran çıktılarında görüldüğü üzere fazla bir tanımlama yükü ile uğraşmadan publish işlemini gerçekleştirebiliyoruz.  
  
  
![image](/image/AzureFunctionsVS/Screenshot_9.jpg)    
  
  

![image](/image/AzureFunctionsVS/Screenshot_10.jpg)  
  
  

![image](/image/AzureFunctionsVS/Screenshot_11.jpg)
  
  
Azure portale girip baktığımızda yaptığımız publish'i kontrol edebilir ve gerekiyorsa düzenleme yapabiliriz.  
  
  

![image](/image/AzureFunctionsVS/Screenshot_12.jpg)  
  
  
Yazdığımız fonksiyonun tanım dosyası function.json  

![image](/image/AzureFunctionsVS/Screenshot_13.jpg)  
  
    
  
  
Not:  

function.json içerisindeki generatedBy satırını silmeniz gerekiyor bu şekilde kullanıma başlayabilirsiniz.  



İyi günler.

