[Ana Sayfa](https://enginunal.github.io/)

# Azure Serverless Mimarisi Üzerinde Azure Functions Örneği – HttpTrigger

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
Bunun için daha önceden bir hesabınız yoksa https://portal.azure.com adresinden deneme süresi boyunca kullanabileceğiniz bir 
hesap açabilirsiniz. Hesap adımını halletiysek adım adım ilerleyerek başlayalım.  

## Portal Üzerinden Azure Function App Oluşturulması

Azure portaline girdikten sonra azure functions oluşturmak için sol üst köşedeki + New ile Azure Marketplace içinden 
Compute altındaki Function App menüsüne giriyoruz.  

![image](https://2.bp.blogspot.com/-szS9mJKZESI/Wl3_NyGrh0I/AAAAAAAAAd0/30mpjL7C-68oJh_3pyF4NN4QWH8fsCp3wCLcBGAs/s1600/Screenshot_1.jpg)    


Bu ekrandan App name ile uygulamamıza isim veriyoruz, varsa mevut bir resource group yoksa new ile yeni yaratıp Create ile devam ediyoruz.  

![image](https://4.bp.blogspot.com/-e1eGHDbpsOE/Wl3_XvE7ynI/AAAAAAAAAd4/adZjsmpqSAQLx8zpYzjdkgC5qgW59qBkQCLcBGAs/s1600/Screenshot_2.jpg)  

Oluşturma işlemi sonlandığında aşağıdaki gibi mesaj gösterecektir. Go to resource ile fonksiyon ekranına gidiyoruz.  

![image](https://1.bp.blogspot.com/-JXnv7NJvaoc/Wl3_ex1qCMI/AAAAAAAAAd8/csNwi9YZ71I8c4rKSzYJc6cDMemX1dItQCLcBGAs/s1600/Screenshot_3.jpg)  

İsmini portalfunctest verdiğimiz uygulamamızın ekranında Functions üzerine gelerek + ‘ya tıkladığımızda yeni fonksiyon yaratma ekranı gelecektir. Bu adımda sağdaki ekrandan alttaki Custom Function’a tıklayarak devam ediyoruz. Custom olarak değil ön tanımlı senaryoları da kullanarak devam edebilirsiniz ben bu örnekte custom üzerinden gideceğim.  

![image](https://4.bp.blogspot.com/-bLwwYkvrcZY/Wl3_nXpaCAI/AAAAAAAAAeA/fhYpYKsJ-1EmVQWqaVY23JIABHxrblS1gCLcBGAs/s1600/Screenshot_4.jpg)  

Gelen şablonlar arasından HTTP trigger şablonunu ve dil olarak C# seçimi yapıyoruz.   

![image](https://1.bp.blogspot.com/-HsVHT5p1ZTw/Wl3_wW6Zg1I/AAAAAAAAAeI/3cJcDMmFRB0YOKLWrgCVlC4Fnu_qoTCzACLcBGAs/s1600/Screenshot_5.jpg)

Devamında trigger tanım ekranından trigger ismi veriyoruz. Benim örneğimde bu isim IsmeMesaj olarak verildi. Create ile işleme devam edip fonksiyon yaratma işleminin sonuna geliyoruz.  

![image](https://2.bp.blogspot.com/-Z58oz50fBLY/Wl3_5v5JsgI/AAAAAAAAAeM/ZWrcTlaCeuggXSnXvLl07flmLRnsEX1cQCLcBGAs/s1600/Screenshot_6.jpg)  

Karşımızda aşağıdaki gibi bir ekran çıkacaktır. Burada csx dosyasının içerisinde fonksiyonda ne yapılması isteniyorsa eklenebilir.  

![image](https://1.bp.blogspot.com/-Qg1WHfVyhjA/Wl4AAJppu3I/AAAAAAAAAeQ/aULN-gHQY7oTQQwniO9CELK4gVy5cy9FACLcBGAs/s1600/Screenshot_7.jpg)

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


![image](https://1.bp.blogspot.com/-a0I_jI8Bjoo/Wl4AU8oEcWI/AAAAAAAAAeY/0HryAXMAL4wR1KxvYBKjqsGQurDxlv9OQCLcBGAs/s1600/Screenshot_8.jpg)  

Ve IsmeMesaj fonksiyonumuza tıklayarak kodlama ve test ekranına gelip test işlemini yapabiliriz.  

![image](https://4.bp.blogspot.com/-QQ19k4ZPEM8/Wl4Ace9ntXI/AAAAAAAAAec/FHA53b-c8dIlfReuocfAgGjdZ7L0NkCQgCLcBGAs/s1600/Screenshot_9.jpg)  

Artık Azure Functions uygulamamız hazır. Bu uygulamayı test değil dışarıdan kullanmak istediğimizde ise sağ üstteki “Get Function URL” ile gerçek ortamdaki url bilgisini alabilir ve erişebiliriz.  
Geliştirdiğimiz fonksiyon için url bilgisi:  

![image](https://4.bp.blogspot.com/-YBFHT-fr54Q/Wl4A3kjMaDI/AAAAAAAAAes/tEOVq6agBTgFKx3SCU6GQsjbpLvqLQKSQCLcBGAs/s1600/Screenshot_11.jpg)  

Ve bunu Postman uygulamasıyla denediğimizde çıktısı ise aşağıdaki gibi olmaktadır.  

![image](https://4.bp.blogspot.com/-ilrINh4q8do/Wl4AjB3tq3I/AAAAAAAAAeg/L4jTFlc4o3UmukeSpkxfrnYtmM2PPtOJACLcBGAs/s1600/Screenshot_10.jpg)  

Geliştirdiğimiz bu fonksiyon uygulamasının OpenAPI tanımlamalarını da yapabiliriz. OpenAPI ile ilgili bu yazıda bir detay bulunmamakta.   
Kısaca tanımlamak gerekirse. OpenAPI Spesifikasyonu (OAS), bir hizmetin kaynak koduna, ek dokümantasyona veya ağ trafiğinin incelenmesine gerek duymadan yeteneklerinin ve özelliklerinin anlaşılmasına olanak tanıyan bir standart sunmaktadır. Şimdilik projemize nasıl eklendiği ile ilgili bilgi verip konuyu sonlandıracağım.
portalfunctiontest ekranına gelip Platform features ve buradaki API definition ekranından,  

![image](https://1.bp.blogspot.com/-mNm874ZLgn4/Wl4ArG-VvAI/AAAAAAAAAek/XjeBDjXGKQIJTMgoR87dGQqxgTfJi99wACLcBGAs/s1600/Screenshot_12.jpg)  

Açılan ekranda API definition source altındaki Function düğmesiyle OpenAPI tanım ekranı açılır.  

![image](https://1.bp.blogspot.com/-SD2aaMvcWBU/Wl4BE8hHsEI/AAAAAAAAAew/Du1wqP22p2Mydgo4uc_c4j8jd4RbGXI6ACLcBGAs/s1600/Screenshot_13.jpg)  

Bu ekrandan Generate API definition template ile api tanımı, şablondan ürettirilir. Bu işlem sonrasında azure functions.json isminde openAPI tanım dosyası oluşturur.   
Oluşturulan tanım dosyası swagger gibi OpenAPI editörleri ile düzenlenebilir.  

Bu yazının devamında aynı işlemin visual studio ile nasıl yapıldığı bilgisini de yakın zamanda paylaşıyor olacağım.  


