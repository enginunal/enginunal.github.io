[Ana Sayfa](https://enginunal.github.io/)

# Galera İle Database Clustering (Veritabanı Kümeleme) Ve MariaDB  
  
  
Veritabanı kümeleme, kısaca verilerinizi depolamak için birden çok bilgisayarın birlikte çalışması ve bu işi yapan bir küme oluşturmalarıdır. Bu tip kümelemeler bize veritabanı ile çalışırken olmasını istemediğimiz durumlara(çökme, veri kayıpları vb.) karşı çözümler sunar ve ölçekleme, monitör etme, yüksek ulaşılabilirlik(high availability) özellikleri ile tercih nedenidirler. 
Bu sistemlerde küme üyeleri arasında senkronizasyon sağlandığından kümeden bir bilgisayarın erişilemez olması durumunda sistemin işleyişi kesintiye uğramaz ve devam eder, bu bize yüksek ulaşılabilirlik sunmaktadır.  

Cluster içerisine aldığımız node'lara bir load balancer yardımı ile işlem yükünün dağıtılabilmesi imkanı da ölçeklemeye örnek olarak verilebilir.Bu ve buna benzer faydalar sıralanabilir fakat bu yazının konusu olmadığından terminoloji ile devam edelim.  

Bir database cluster, node ismi verilen ve bağımsız database sunucusu olarak tanımlayabileceğimiz yapılardan oluşur. Node'ları üzerinde veritabanı sunucusu yüklü bilgisayarlar olarak düşünürsek cluster'ı birbirine bağlı bilgisayarların oluşturduğu küme olarak düşünebiliriz. Node'ların iletişimini ve yönetimini cluster yönetim yazılımları yapmaktadır.  
Node'ların ayrı ayrı işletim sistemine sahip makinalar oldukları örneğini vermiştim fakat bir işletim sistemi üzerinde birden çok veritabanı sunucusu kurulabilme imkanı vardır bu durumda tek makina üzerinde birden çok node da olabilir fakat önerilmez. Nedeni ise o makina çöktüğünde onunla birlikte taşıdığı node'lar da çökecektir.  


#### Node'lar kendi arasında ikiye ayrılırlar:  
  
#### 1- Master Node  
Veritabanına yazma ve okuma hakkı bulunan node'lardır. Eğer veritabanına bir kayıt eklemek isteniliyorsa master node üzerinden yapılır. Devamında slave node bu bilgiyi master node'dan alır ve kaydeder.  
  
  
#### 2- Slave Node  
Veritabanından sadece okuma hakkı olan node'lardır. Slave node, master node tarafından yazılan veriyi alır ve kendi veritabanına kaydeder.  
  
  

#### Cluster Topolojisi ikiye ayrılır:  
  
  
#### 1- Master-master(veya multi-master) cluster  
Cluster içerisindeki her node veritabanına kaydetmeye yetkilidir ve herhangi bir node yazma işlemi için kullanılabilir.  
  
  
#### 2- Master-slave cluster  
Sadece master node'lar veritabanına yazma yetkisine sahiptir, slave node'lar sadece okuma yapabilir.  
  
  
Bu kısa özetten sonra Galere Cluster konusuna giriş yapabiliriz.  


  
### Galera Cluster  
  

([Galera Cluster](http://galeracluster.com/products/)), multi-master topolojisinde çalışan ve veritabanı replikasyon senaryosu olarak senkronize olarak master node'lar arasında dağıtan mimariye sahiptir.   
Minimum konfigürasyonda cluster en az 3 node içermelidir. Daha çok node içeren cluster için node sayısının tek sayı olması öneriliyor.  

>Not:  
Replikasyon için veri transferi iki yöntemle gerçekleşir senkron ve asenkron.  
Senkron veri transferinde(Galera'da olduğu gibi) veriler node'lar arasında transfer edilir ve işlemin bitmesi beklenir, replikasyon işlemi gerçek zamanlı yapılmaktadır.   
Asenkron transfer işleminde veritabanı replikasyonu işleminde bekleme olmadan arka planda gerçekleşir, işlemin bitmesi beklenmemektedir. Örneğin node'ler arasında uzak mesafeler olduğunda veya bağlantının zayıf olduğu durumlarda veya işlemin tamamlanmasının beklenemeyecek kadar uzun süreceği durumlarda kullanılır. veritabanı yedekleme vb işlemlerde de sıkça kullanılır.  


Galera'nın avantajları nedir? Özet olarak senkron replikasyon, aktiv multi-master topolojisi, herhangi bir node üzerinden okuma ve yazma yapılabilme, otomatik node ekleme, satır seviyesinde(row level) paralel replikasyon gibi sıralanabilir.  


### MariaDB  

([MariaDB](https://mariadb.org/)) açık kaynaklı bir RDBMS yani ilişkisel veritabanı sunucusudur.  
MySQL'in geliştiricisi ([Michael Widenius (Monty)](https://en.wikipedia.org/wiki/Michael_Widenius)) tarafından geliştirilmiş ve GNU GPL lisansı ile yayınlanmıştır. MySQL ile aynı altyapı üzerinde çatallanmış(fork) bir proje olduğundan MySQL ile uyumlu araçları ve komutları da destekler. Bu nedenle MySQL kullanan sistemlerden geçişi kolay olmaktadır.  


## Kurulum ve Konfigürasyon İşlemleri  

Yukarıda geçtiğim kısa özetlerden sonra sistemimize önce mariadb sunucularını kurup devamında galera cluster kurulum ve konfigürasyonunu yapıp tüm bunların denemesini yapacağız. Kullandığım sistem Ubuntu 18.04 versiyonu, mariadb 10.3 versiyonudur, galera cluster mariadb kurulumu içerisinde gelmektedir(10.1'den itibaren geliyor).  
MariaDB kurulumu ile başlayalım.  


### MariaDB Kurulumu

Son versiyon olan 10.3'ü yüklemek için repository tanımını yapmamız gerekir, eğer 10.1 kullanılacaksa bu tanımı yapmadan doğrudan apt install ile kurulabilmekte. Ben örnekte 10.3 versiyonunu kullanacağım.  
  
Aşağıdaki komutlar sırayla çalıştırılır.  

```
sudo apt-get install software-properties-common
```

```
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
```

```
sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el] ftp://ftp.ulak.net.tr/pub/MariaDB/repo/10.3/ubuntu bionic main'
```

```
sudo apt update
```

```
sudo apt install mariadb-server
```

MariaDB sunucusunu kurmayı tamamladık servisin durumunu kontrol edelim.  

```
sudo systemctl status mariadb
```

Eğer kendiliğinden başlamadıysa.  

```
sudo systemctl start mariadb.service
sudo systemctl enable mariadb.service
```

Komutları ile başlatıp otomatik başlatma tanımı yapabiliriz.Kurduğumuz sunucunun versiyonunu kontrol edelim.   

```
mysql -V
```

Bu işlemlerden sonra MariaDB güvenliği için bir yardımcı olan scripti çalıştıralım.  

```
sudo mysql_secure_installation
```

Kurulum ve konfigürasyonu tamamladık. Artık veritabanı sunucumuz ile iletişime geçip işlemlerimizi gerçekleştirebiliriz.  
Bunun için arayüze ulaşım yöntemi:  

```
mysql -u root -p
```

Sunucudaki veritabanlarını listeletelim.  

```
MariaDB [()]> show databases;
```

Komutun çıktısı:  

```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.000 sec)
```

Yeni bir veritabanı yaratma komutu.  

```
MariaDB [()]> create database deneme_db default character set utf8 default collate utf8_bin;
```

Tekrar show databases yaparsak veritabanımız listenelecektir.  

```
MariaDB [(none)]> show databases;
```

Komutu çıktısı:  

```
+--------------------+
| Database           |
+--------------------+
| deneme_db          |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.000 sec)
```

Yarattığımız veritabanı için bir kullanıcı yaratalım ve yetki verelim.  

```
MariaDB [()]> GRANT ALL PRIVILEGES ON deneme_db.* to deneme_kul@'%' IDENTIFIED BY 'sifre_123';
MariaDB [()]> GRANT ALL PRIVILEGES ON deneme_db.* to deneme_kul@'localhost' IDENTIFIED BY 'sifre_123';
```

Verdiğimiz yetkilerin aktifleştirilmesi için:  

```
MariaDB [()]> FLUSH PRIVILEGES;
```

Yetkileri kontrol edelim:  

```
MariaDB [()]> SHOW GRANTS FOR 'deneme_kul'@localhost;
```

Komutun çıktısı:  
```
+-------------------------------------------------------------------------------------------------------------------+
| Grants for deneme_kul@localhost                                                                                   |
+-------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'deneme_kul'@'localhost' IDENTIFIED BY PASSWORD '*433EB8B719B7D5EFEE4D6FE9DCB6813F15C1B217' |
| GRANT ALL PRIVILEGES ON `deneme_db`.* TO 'deneme_kul'@'localhost'                                                 |
+-------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.000 sec)
```

Kullanıcı ve veritabanı silme işlemleri için:  

```
MariaDB [()]> DROP USER deneme_kul@localhost;
MariaDB [()]> DROP DATABASE deneme_db;
```

Çıkış için:  

```
MariaDB [()]> quit
```


Evet MariaDB kurulumunu tamamlayıp test ettik sorunsuz çalışıyor. Artık galera cluster oluşturabiliriz.  
  
  

### Galera Cluster Kurulumu   

Öncelikle bu mimariyi ayağa kaldırırken en az üç node olmalı fakat ben sadece örnek olarak bu işi yapacağımdan iki node ile bir cluster ayağa kaldırıp denemesini yapacağım. Elimde iki node var bunlar:  

| HostName | IP |
| --- | --- |
|vboxeul	| 192.168.99.100 |
|vboxeul1	| 192.168.99.101 |
  
  
vboxeul olan cluster tanımını yapacağım master node olacak.  
Konfigürasyonumuzu yapmaya başlayalım.

```
eul@vboxeul:~$ sudo nano /etc/mysql/mariadb.cnf
```

Komutu ile master node olan ilk nodu'umuzun konfigürasyonunu gerçekleştireceğiz dosya içerisindeki character_set_server tanımlarını aşağıdaki gibi açıyoruz.  

```
character_set_server   = utf8
```

İşlem sonunda dosya aşağıdakine benzemeli.  


```
# MariaDB-specific config file.
# Read by /etc/mysql/my.cnf

[client]
# Default is Latin1, if you need UTF-8 set this (also in server section)
default-character-set = utf8

[mysqld]
#
# * Character sets
# 
# Default is Latin1, if you need UTF-8 set all this (also in client section)
#
character-set-server  = utf8
#collation-server      = utf8_general_ci 
character_set_server   = utf8
#collation_server       = utf8_general_ci 
# Import all .cnf files from configuration directory
!includedir /etc/mysql/mariadb.conf.d/
```

Ve galera konfigürasyon dosyasını oluşturmaya başlayacağız. Aşağıdaki gibi galera.cnf dosyasını ekliyoruz.  

```
eul@vboxeul:~$ sudo nano /etc/mysql/mariadb.conf.d/galera.cnf
```

Bu dosya içerisinde wsrep_cluster_address, wsrep_node_address ve wsrep_node_name alanlarına kendi node'larımıza ait tanımlamaları yapıyoruz ve dosyayı kaydediyoruz.  

Tanım dosyası aşağıdakine benzer olmalı.  

```
[mysqld]
bind-address=0.0.0.0
default_storage_engine=InnoDB
binlog_format=row
innodb_autoinc_lock_mode=2

# Galera cluster configuration
wsrep_on=ON
wsrep_provider=/usr/lib/galera/libgalera_smm.so
wsrep_cluster_address="gcomm://192.168.99.100,192.168.99.101"
wsrep_cluster_name="mariadb-galera-cluster"
wsrep_sst_method=rsync

# Cluster node configuration
wsrep_node_address="192.168.99.100"
wsrep_node_name="vboxeul"
```

Cluster tanımını yaptık şimdi de vboxeul1 node'una geçip konfigürasyonu orada da tanımlayalım. Aynı vboxeul node'unda yaptığım gibi galera.cnf dosyasını oluşturacağım.  

```
eul@vboxeul1:~$ sudo nano /etc/mysql/mariadb.conf.d/galera.cnf
```

Dosyanı geneli cluster node'daki ile aynı sadece Cluster Node Configuration bölümünde node'a ait tanımları düzenliyoruz ve kaydediyoruz. vboxeul1 node'u için ip adresi 192.168.99.101 idi.  

```
[mysqld]
bind-address=0.0.0.0
default_storage_engine=InnoDB
binlog_format=row
innodb_autoinc_lock_mode=2

# Galera cluster configuration
wsrep_on=ON
wsrep_provider=/usr/lib/galera/libgalera_smm.so
wsrep_cluster_address="gcomm://192.168.99.100,192.168.99.101"
wsrep_cluster_name="mariadb-galera-cluster"
wsrep_sst_method=rsync

# Cluster node configuration
wsrep_node_address="192.168.99.101"
wsrep_node_name="vboxeul1"
```


Konfigürasyon işlemleri bitti şimdi ilk node'umuza gidip mariadb servisini kapatalım.  

```
eul@vboxeul:~$ sudo systemctl stop mariadb
```

Ve yeni galera cluster'ımızı başlatalım.  

```
eul@vboxeul:~$ sudo galera_new_cluster
```

Galera cluster çalışıyor mu kontrol etmek için:  

```
eul@vboxeul:~$ mysql -u root -p -e "show status like 'wsrep_%'"
```

komut çıktısı:  

```
Enter password: 
+------------------------------+-----------------------------------------------+
| Variable_name                | Value                                         |
+------------------------------+-----------------------------------------------+
| wsrep_apply_oooe             | 0.000000                                      |
| wsrep_apply_oool             | 0.000000                                      |
| wsrep_apply_window           | 0.000000                                      |
| wsrep_causal_reads           | 0                                             |
| wsrep_cert_deps_distance     | 0.000000                                      |
| wsrep_cert_index_size        | 0                                             |
| wsrep_cert_interval          | 0.000000                                      |
| wsrep_cluster_conf_id        | 1                                             |
| wsrep_cluster_size           | 1                                             |
| wsrep_cluster_state_uuid     | 9e916cd1-c6e4-11e8-8f7b-5b7186e33269          |
| wsrep_cluster_status         | Primary                                       |
| wsrep_commit_oooe            | 0.000000                                      |
| wsrep_commit_oool            | 0.000000                                      |
| wsrep_commit_window          | 0.000000                                      |
| wsrep_connected              | ON                                            |
| wsrep_desync_count           | 0                                             |
| wsrep_evs_delayed            |                                               |
| wsrep_evs_evict_list         |                                               |
| wsrep_evs_repl_latency       | 2.567e-06/5.6892e-06/1.1552e-05/3.27278e-06/5 |
| wsrep_evs_state              | OPERATIONAL                                   |
| wsrep_flow_control_paused    | 0.000000                                      |
| wsrep_flow_control_paused_ns | 0                                             |
| wsrep_flow_control_recv      | 0                                             |
| wsrep_flow_control_sent      | 0                                             |
| wsrep_gcomm_uuid             | 9e902a58-c6e4-11e8-97e3-8ffed84664cb          |
| wsrep_incoming_addresses     | 192.168.99.100:3306                           |
| wsrep_last_committed         | 0                                             |
| wsrep_local_bf_aborts        | 0                                             |
| wsrep_local_cached_downto    | 18446744073709551615                          |
| wsrep_local_cert_failures    | 0                                             |
| wsrep_local_commits          | 0                                             |
| wsrep_local_index            | 0                                             |
| wsrep_local_recv_queue       | 0                                             |
| wsrep_local_recv_queue_avg   | 0.500000                                      |
| wsrep_local_recv_queue_max   | 2                                             |
| wsrep_local_recv_queue_min   | 0                                             |
| wsrep_local_replays          | 0                                             |
| wsrep_local_send_queue       | 0                                             |
| wsrep_local_send_queue_avg   | 0.500000                                      |
| wsrep_local_send_queue_max   | 2                                             |
| wsrep_local_send_queue_min   | 0                                             |
| wsrep_local_state            | 4                                             |
| wsrep_local_state_comment    | Synced                                        |
| wsrep_local_state_uuid       | 9e916cd1-c6e4-11e8-8f7b-5b7186e33269          |
| wsrep_protocol_version       | 7                                             |
| wsrep_provider_name          | Galera                                        |
| wsrep_provider_vendor        | Codership Oy <info@codership.com>             |
| wsrep_provider_version       | 3.20(r7e383f7)                                |
| wsrep_ready                  | ON                                            |
| wsrep_received               | 2                                             |
| wsrep_received_bytes         | 145                                           |
| wsrep_repl_data_bytes        | 0                                             |
| wsrep_repl_keys              | 0                                             |
| wsrep_repl_keys_bytes        | 0                                             |
| wsrep_repl_other_bytes       | 0                                             |
| wsrep_replicated             | 0                                             |
| wsrep_replicated_bytes       | 0                                             |
| wsrep_thread_count           | 2                                             |
+------------------------------+-----------------------------------------------+
```

Evet cluster'ımız sağlıklı ve çalışır durumda. İlk aşamada daha diğer node eklenmediğinden cluster size değeri 1 olmalı onu da kontrol edelim.  

```
eul@vboxeul:~$ mysql -u root -p -e "show status like 'wsrep_cluster_size'"
```

Komutu çıktısı:  

```
Enter password: 
+--------------------+-------+
| Variable_name      | Value |
+--------------------+-------+
| wsrep_cluster_size | 1     |
+--------------------+-------+
```

Şimdi diğer node'umuz olan vboxeul1'e geçip mariadb servisini çalıştıracağız ve cluster size'a orada tekrar bakıp 2 olduğunu görebiliriz.  

```
eul@vboxeul1:~$ sudo systemctl stop mariadb
eul@vboxeul1:~$ sudo systemctl start mariadb
eul@vboxeul1:~$ mysql -u root -p -e "show status like 'wsrep_cluster_size'"
```

Komutu çıktısı:  

```
Enter password: 
+--------------------+-------+
| Variable_name      | Value |
+--------------------+-------+
| wsrep_cluster_size | 2     |
+--------------------+-------+
```

Cluster'ımızın tanımlarını yaptık ve node'larımız eklendi. Artık sistemin çalıştığını test edebiliriz.  


##### Galera Cluster Test İşlemi  

vboxeul node'unda bir veritabanı yaratıp vboxeul1 node'undan bunu gözlemleyeceğiz.  

```
eul@vboxeul:~$ mysql -u root -p
```

ile galera cluster'a root olarak girelim.Sonrasında engin_test veritabanını create database engin_test; komutu ile yaratalım.  

```
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 41
Server version: 10.3.9-MariaDB-1:10.3.9+maria~bionic-log mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> create database galera_test;
Query OK, 1 row affected (0.008 sec)
```

Şimdi gidip vboxeul1 node'undan veritabanlarını listeleyip burada yarattığımız engin_test veritabanını görmeye çalışalım.  

```
eul@vboxeul1:~$ mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 41
Server version: 10.3.9-MariaDB-1:10.3.9+maria~bionic-log mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| engin_test         |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.001 sec)
```

```
MariaDB [(none)]> exit
Bye
```


engin_test veritabanımız vboxeul node'unda yaratıldı ve vboxeul1 node'una da replike edildi.  
  
  
Cluster oluşturma işlemini tamamlamış olduk. Bu işlemin devamında sisteme database proxy eklenmesi ve load balancing gibi konular da gelmekte umarım ilgili bir başka yazıda görüşmek üzere.


Engin ÜNAL







