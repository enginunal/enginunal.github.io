[Ana Sayfa](https://enginunal.github.io/)

# Repository ve Unit Of Work Tasarım Kalıbı ve Uygulanması  


Bu yazıda Repository design pattern konusunu anlatmaya çalışacağım, bunun yanında Unit Of Work pattern konusunda da kısa bir özet geçip kod örneği ile yazıyı uzatmadan tamamlamış olacağım.
Yazıyı hazırlarken kullandığım geliştirme ortamı .Net Framework ve C#. Bu nedenle öncelikle DbContext nedir? Bu noktadan başlayalım.  

## DBContext  

Veritabanına karşılık gelen obje yapısıdır. İçinde tablo yapısında karşılık gelen DbSet objelerini bulundurur.  

DbContext kullanarak tablo ve view yapılarına erişebilir, DbSet yapısını kullanarak tablo üzerinde CRUD işlemlerini gerçekleştirebilirsiniz.  


## Repository Tasarım Kabılı (Repository Design Pattern)  

Repository temel olarak veritabanı sorgulama işlemlerinin bir merkezden yapılmasını sağlayarak iş katmanına bu işlerin taşınmasını önler bu şekilde sorgu ve kod tekrarına engel olmuş olur. Yani asıl amaç veri işlem ve sorgulamaların tekrarlardan kaçınılarak merkezi bir yapıya çekilmesidir. Bu sayede veritabanı işlemlerimizi tekrar ve tekrar iş katmanı içinde yazmak durumununda kalmaktan uzak dururuz.  

Repository tasarım kalıbının ilk ve en önemli amacı budur, bunun yanında yukarıdaki tanıma ek olarak repository tasarım kalıbı, programınızda asıl işi yapan bölümler ile veriye erişen bölümlerin birbirinden soyutlanması mantığını da getirmiştir. Yani veri katmanı ve bu katmanı kullanan iş katmanı arasında bir arabirim olarak yer alır ve bu iki katman arasında soyutlama görevi de üstlenir.  

Repository tasarım kalıbı ile ilgili yazılan her yazıda olduğu gibi Martin Fowler'den özlü sözler köşesi olmazsa olmazdır.  

Martin Fowler repository tanımı için der ki:  

"Mediates between the domain and data mapping layers using a collection-like interface for accessing domain objects."  

"Conceptually, a Repository encapsulates the set of objects persisted in a data store and the operations performed over them, providing a more object-oriented view of the persistence layer. Repository also supports the objective of achieving a clean separation and one-way dependency between the domain and data mapping layers."  


Bir çok yazının olmazsa olmazı aşağıdaki repository şemasını da eklemeliyim.  

![image](https://3.bp.blogspot.com/-5ZhIqOImL1E/Wh0KGkAXuaI/AAAAAAAAAc8/Aqsb7OWrIyAQ-NYtRN6_-UHm1YtSOweggCLcBGAs/s320/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)  
Resim microsoft asp.net konu anlatımı kısmından alınmıştır.  
  
  
Şema, repository kullanımının ve araya katmanlar koymanın bize nasıl modüler bir yapı sunduğunu ortaya koymaktadır. En soldaki kısım repository kullanılmadığı durumlarda doğrudan veritabanına dbcontext aracılığı ile erişilmesini göstermekte. Sağdaki kısımda ise Unit Of Work pattern kullanılarak katmanlarla ayrılan EF ve Controller bölümlerinin arasına istenildiği anda gerçek repository değil bir moc repository yerleştirme sayesinde test edilebilirliğin artması görülebilmektedir.  


Repository dediğimiz kalıp nedir? Neler içermelidir?  
Repository tanım gereği objeler içeren bir collection yapısındadır. Bu objeler memory'de tutulur ve objelere erişmek için collection nesnesinde kullandığımız bazı ortak metodları kullanırız. Bu metodlar add, remove, get, getAll, find olarak örneklendirilebilir. Dikkat ederseniz metodlar arasında save veya update bulunmamakta. Bunun nedeni ise repository bir obje koleksiyonu olduğundan görevi veritabanını güncellemek veya ona birşey eklemek değildir.  

Elimizdeki obje koleksiyonu üzerinde işlemlerimizi gerçekleştiririz ve bu objelerdeki değişikliklerin veritabanına aktarılması işlemini unit of work tasarım kalıbı ile gerçekleştiririz.  

Bu aşamada Unit Of Work tasarım kalıbı nedir? Bunu öğreneceğiz.  


## Unit Of Work Tasarım Kalıbı (Unit Of Work Design Pattern)  

Bir transaction tarafından etkilenen nesnelerin listesini tutar ve değişikliklerin yazılması ile eşzamanlılık sorunlarının çözümünü koordine eder.  

Martin Fowler der ki:  

"Maintains a list of objects affected by a business transaction and coordinates the writing out of changes and the resolution of concurrency problems."  

"A Unit of Work keeps track of everything you do during a business transaction that can affect the database. When you're done, it figures out everything that needs to be done to alter the database as a result of your work."  


Uzun uzun teorik bilgilere boğulmak yerine hemen kod örneklerine geçip yukarıda anlattığım konuların pratikteki karşılıklarını incelemek daha yararlı olacaktır. Bu bilgiler ışığında kod örneklerine geçelim. Öncelikle basit bir model kodlayalım.  


    public class Kisi
    {
        public int Id { get; set; }
        public string Ad { get; set; }
        public string Soyad { get; set; }
    }



Kişi modelimiz için DbContext hazırlayalım.

```
    public class KisiDbContext : DbContext
    {
        public virtual DbSet Kisiler { get; set; }

        public KisiDbContext(string nameOrConnectionString) : base(nameOrConnectionString)
        {
        }               
     }
```


Örnek model ve DbContext yapımız hazır. Artık repository kodlamasına geçebiliriz. ortak kullanılabilecek yapı olan Generic Repository Interface kodlamasını yapalım.  

```
    public interface IRepository where TEntity : class
    {
        TEntity Get(int id);
        IEnumerable GetAll();
        IEnumerable Find(Expression&gt; predicate);

        void Add(TEntity entity);
        void AddRange(IEnumerable entities);

        void Remove(TEntity entity);
        void RemoveRange(IEnumerable entities);
    }
```


Şimdi bu interface implementasyonunu gerçekleştirelim.  

```
    public class Repository : IRepository where TEntity : class
    {
        protected readonly DbContext Context;


        public Repository(DbContext context)
        {
            Context = context;
        }

        public void Add(TEntity entity)
        {
            Context.Set().Add(entity);
        }

        public void AddRange(IEnumerable entities)
        {
            Context.Set().AddRange(entities);
        }

        public IEnumerable Find(Expression&gt; predicate)
        {
            return Context.Set().Where(predicate);
        }

        public TEntity Get(int id)
        {
            return Context.Set().Find(id);
        }

        public IEnumerable GetAll()
        {
            return Context.Set().ToList();
        }

        public void Remove(TEntity entity)
        {
            Context.Set().Remove(entity);
        }

        public void RemoveRange(IEnumerable entities)
        {
            Context.Set().RemoveRange(entities);
        }
    }
```



Görüldüğü üzere, repository içerisinde save veya update metodları bulunmuyor. Tasarımın kurallarına tam olarak uyulduğunda bu şekilde kodlamak gerekir. Bunun yanında dikkat çeken başka önemli nokta ise entity listesini IQueryable değil IEnumerable olarak döndürmekteyiz. Bunun nedeni IQueryable kullanmanın repository design pattern tasarımına aykırı olmasıdır. IQueryable kullanırsak bu repository'i kullanan üst katmanların bu interface'e sorgular üretip göndermesine imkan tanımış olur ve tasarımda delik açmış oluruz.Sorgulama işlemleri repository içinde yapılmalıdır.  


Yukarıda tanımını yaptığımız generic repository'den Kişileri çekebileceğimiz yapı üretmek üzere KişilerRepository türetelim. Öncelikle IRepositoryKisiler interface tanımlamasını yapalım. Interface içine örnek olsun diye sadece kişi listesini alabileceğim bir metod ekleyeceğim.  

```
    public interface IKisilerRepository : IRepository
    {
        IEnumerable KisileriGetir();

    }
```


Görüldüğü gibi IKisilerRepository interface'i IRepository generic repository'den türemekte ve Kişi tipini almaktadır. İmplementasyonu gerçekleştirelim.  

```
    public class KisilerRepository : Repository, IKisilerRepository
    {
        public KisiDbContext KisiDbContext
        {
            get { return Context as KisiDbContext; }
        }

        public KisilerRepository(KisiDbContext context) : base(context)
        {
        }

        public IEnumerable KisileriGetir()
        {
            return KisiDbContext.Kisiler;
        }
    }
```


KisilerRepository class'ı Repository class'ından türemekte ve IKisilerRepository interface'ini implemente etmekte. Repository'lerimizi tanımladık ve ne işle yaradıklarını görmüş olduk. Devamında persistence işlemlerini gerçekleştirebileceğimiz unit of work yapısını oluşturmayı inceleyelim.  

Öncelikle IUnitOfWork interface tanımlamasını yapalım.  


```
    public interface IUnitOfWork : IDisposable
    {
        IKisilerRepository Kisiler { get; }
        int Complete();
    }
```

IUnitOfWork interface'i Kisiler repository'i dışa aktarır. Bunun getirdiği fayda ise test süreçlerinde Mock Interface ile yer değiştirip gerçek repository'ler yerine mock repository'lerin kullanılarak test yapılmasını sağlamaktır.  

Bu interface implementasyonu aşağıdaki gibidir.  


```
    public class UnitOfWork : IUnitOfWork
    {
        private readonly KisiDbContext _context;

        public UnitOfWork(KisiDbContext context)
        {
            _context = context;
            Kisiler = new KisilerRepository(_context);
        }

        public IKisilerRepository Kisiler { get; private set; }

        public int Complete()
        {
            return _context.SaveChanges();
        }

        public void Dispose()
        {
            _context.Dispose();
        }
    }
```


Tüm interface ve class tanımlamalarımızı yaptık. Bu yapıyı nasıl kullanacağız? Bunun için kısa bir örnek:  

```
using (var unitOfWork = new UnitOfWork(new KisiDbContext("denemedb") ) )
{
  unitOfWork.Kisiler.Add(new Kisi() { Id = 1, Ad = "Engin", Soyad = "Ünal" });
  unitOfWork.Kisiler.Add(new Kisi() { Id = 2, Ad = "Ali", Soyad = "Veli" });
  unitOfWork.Kisiler.Add(new Kisi() { Id = 3, Ad = "Zeki", Soyad = "Metin" });

  Kisi[] kisiler = unitOfWork.Kisiler.KisileriGetir().ToArray();

}
```











