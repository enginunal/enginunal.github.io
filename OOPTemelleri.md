[Ana Sayfa](https://enginunal.github.io/)

# C# İle OOP Temelleri  

Bu yazıda OOP(Nesne Yönelimli Programlama) kavramı ve bu kavramla ilgili bilgileri özet olarak vermeye çalışacağım.  
OOP modelinde temel olarak dört konsept bulunmaktadır.  

Aşağıda özetlerini verdiğim konularla ilgili kod örnek projesini incelemek isteyenler için github hesabıma https://github.com/enginunal/OOPBasics repository olarak yükledim.   


## 1. Encapsulation  
Kapsülleme. Sınıf içindeki değişkenleri(variables) ve metodları(methods) gizlemek için kullanılır. Bu elemanların dış erişime kapalı ve korumalı hale getirilip kapsanması işlemidir. Dışarıdan bu elemanlara erişim yardımcı metodlar aracılığı ile kontrollü olarak yapılabilir.  


Örnek:  

```
public class Employee
{
    private string firstName;
    private string lastName;

    public String FirstName
    {
        get { return firstName; }
        set
        {
            firstName = value;
        }
    }

    public String LastName
    {
        get { return lastName; }
        set
        {
            lastName = value;
        }
    }

    public string FullName()
    {
        return string.Format("{0} {1}", firstName, lastName);
    }
}
```


## 2. Abstraction  
Soyutlama. Nesnenin istenmeyen/önemsiz tüm özelliklerini dışa kapatan ve yalnızca dışa açılması gerekli özellikleri açan mekanizmadır. Soyutlama, nesnenin yaptığı işin detayını bilmek yerine nesnelere odaklanmanıza olanak tanır arka planda de olduğunu bilmenize gerek bırakmadan temel özelliği temsil eder ve alakalı bilgiler sağlayarak sınıflarınızın veya nesnelerinizin genel bir görünümünü sağlar. 
Soyutlama, bir nesnenin çalışma biçimini gizleme ve bir nesnenin bilgisini anlaşılabilir bir şekilde gösterme işlemidir.
Veya diğer ifadeyle, soyutlama, bir nesnenin sadece temel özelliklerini gösteren bir mekanizmadır. Amacı, türetilmiş sınıflara işlevsellik sağlamaktır.   

C# dilinde soyutlama soyut sınıf(abstract class) ve soyut yöntemler(abstract functions) kullanılarak gerçekleştirilir.  


Örnek:

```
public abstract class Shape
        {
            private int _width;
            private int _height;

            public int Width
            {
                get { return _width; }
                set { _width = value; }
            }

            public int Height
            {
                get { return _height; }
                set { _height = value; }
            }
            
            public abstract float CalculateArea();
                        
        }

        public class Rectangle : Shape
        {
            public override float CalculateArea()
            {
                return Width * Height;
            }
        }
```


## 3. Inheritance  
Miras. Miras, bir sınıftaki üyeleri yeniden kullanan, genişleten ve değiştiren yeni sınıflar oluşturmanıza olanak tanır. 
Üyeleri devralınan sınıflara temel sınıf(base class), bu üyeleri miras alan sınıf türetilmiş sınıf(derived class) olarak adlandırılır.
Bu özellik kod işlevselliğini yeniden kullanma fırsatı sağlar ve uygulama süresini hızlandırır.  

Örnek:  
Triangle class'ı Shape class'ından türetilmiştir ve onun Width,Height ve ShowDim üyelerini kalıtımsal olarak kendi sınıfında kullanabilir.  

```
        public class Shape
        {
            public double Width;
            public double Height;
            public void ShowDim()
            {
                Console.WriteLine("Width and height are " + Width + " and " + Height);
            }
        }

        public class Triangle : Shape
        {
            public string Style;

            public void ShowArea()
            {
                Console.WriteLine("Area is " +  Width * Height / 2);
            }

            public void ShowStyle()
            {
                Console.WriteLine("Triangle is " + Style);
            }
        }
```


Bu noktada sınıf ve üyelerinin dışarıdan kullanımını kısıtlayabileceğimiz access modifier yapıları bulunmaktadır.
Bu anahtar kelimelerle sınıfımızdaki üyelerin hangi ölçüde paylaşılacağının tanımını yapabiliriz.  

Sınıf elemanlarına 5 tip tanımlayıcı kullanılarak ne ölçüde dışarı açılacağı belirlenir.  
Bu tanımlayıcılar: public, private, internal, protected and protected internal olarak verilmiştir.  

public: Programdaki herhangi bir koddan erişilebilir.  
private: Yalnızca aynı sınıfa ait üyeler tarafından erişilebilir.  
protected: Aynı sınıfa ait üyeler tarafından ve türetilmiş sınıflardan erişilebilir.  
internal:  Sadece aynı assembly içerisinden erişilebilir.  
protected internal: Aynı assembly ve türetilmiş sınıflar içinde erişilebilir.  



## 4. Polymorphism  
Çok biçimlilik. Polimorfizm kelimesi birçok forma sahip olmak demektir. Nesne yönelimli programlama paradigmasında, polimorfizm genellikle 'bir arayüz, birden çok işlev' olarak ifade edilir. Çalışma zamanında temel sınıf başvurusu(base class reference) yoluyla türetilmiş sınıf yöntemlerini çağırmanıza izin verir.  
Aynı adla çağrılan yöntemlerin farklı uygulamalarını sınıflara sunma yeteneğine sahiptir.  
Polimorfizm statik veya dinamik olabilir.  
Statik polimorfizmde, bir işleve verilen yanıt derleme zamanında belirlenir. (overloading)  
Dinamik polimorfizmde, çalışma zamanında karar verilir. (overriding)  

Statik polimorfizm örneği:  

```
	public class Overloading
        {
            public void Add(string a1, string a2)
            {
                Console.WriteLine("Adding Two String :" + a1 + a2);
            }

            public void Add(int a1, int a2)
            {
                Console.WriteLine("Adding Two Integer :" + (a1 + a2));
            }
        }
```  

Dinamik polimorfizm örneği:  

```
	public class Overriding
        {
            public class Base
            {
                public virtual void Show()
                {
                    Console.WriteLine("Show() From Base Class.");
                }
            }

            public class Derived : Base
            {
                public override void Show()
                {
                    Console.WriteLine("Show() From Derived Class.");
                }
            }

        }
```
  
Derived sınıfı, temel sınıfımız olan Base sınıfı tipinde bir nesne olarak saklanabilir.  
  
Örnek:  

```
Base objBase;
objBase = new Base();
objBase.Show();//Output ----> Show() From Base Class.

objBase = new Derived();
objBase.Show();//Output--> Show() From Derived Class.
```


