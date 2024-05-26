# SIC-XE
<hr>
<p>Bu proje SIC/XE mimarisinin pas1 ve pas2 adımlarının python dilindeki gerçekleştirilmesidir. Projenin amacı verilen assembly kodunu işleyerek geçici bir dosyaya ara kod üretmek ve 
bu ara kodu object koda dönüştürmektir.</p>
<h1>Pass1 adımı</h1>
<hr>
<p>pass1 fonksiyonu input_file dosyasından yazılan assembly kodu işleyerek etiket ve adresleri bulmaktayız ve düzenlenen kodu bi ara dosya olan intermediate_file assembly kodu düzenleriz 
bu bize object koda çevirmemizde yani pass2 adımını gerçkleştiremizde yardımcı olucaktır.</p>
<h3>Pass1 fonksiyonun içeriği</h3>
  <ul>
    <li>parse_line fonksiyonu  her satırı ayrıştırır ve etiket opcode ve operand olup olmadığını belirleriz.</li>
    <li>add_symbol  fonksiyonu semmbol tablosuna yeni bir sembol ekler ve onun adresini döndürürüz.</li>
    <li>process_literals  fonksiyonu geçici dosyaya yazılan literalleri işler ve literallerin adreslerini belirler.</li>
    <li>İnput_file Dosyası ile okuma ve intermediate_file dosyasına yazma işlemleri geçrkleştirme işlemlerine başlarız </li>
    <li>yorum satıları boş geçilir ve parse_line fonksiyonu ile alanlar bulunur</li>
    <li>START komutunu bulur ve programın başlangıç adresini belirler. Eğer adres var ise adresi yok ise başlangıç adresi 0 kabul edilir</li>
    <li>Assembly komutlarını ve operantlarını geçici dosyaya yazılır her bir satırın başında program sayacı değeri locctr ile birlikte satırı yazrırız Eğer etiket yoksa boşluk bırakırz.</li>
    <li>Eğer yazılan komut WORD ise yine LOCCTR 3 arttırırız, RESW ve RESB komutları ise belirtilen değer kadar 3 katı ve doğrudan LOCCTR arttırırız BYTE komutu ise verilen byte cinsinden LOCCTR arttırırız.</li>
    <li>komut LTORG ise, literaller işlenir.</li>
    <li>END komutu bulunduğunda işlem sonlandırılır ve program_length ile programın uzunluğu belirlenir.</li>
  </ul>
<br>
<p>pass1 fonksiyonu sonucunda elde ettiğimiz bilgiler şu şekilde olacaktır sembol tablosu ve adres, literal tablosu, program uzunluğu, programın başlangıç adresi, programın adı ve intermediate_file dosyasında assemble kodun düzenlenmiş hali bulunmaktadır bu dosya yorum satılarından arındırılmış adresleri bulunmuş bir biçimde bulunmaktadır (Adres, label, opcode, operand biçimde).</p>
<br>
<br>
<br>
<h1>Pass adımı</h1>
<hr>
<p>Pass2 fonksiyonu intermediate_file dosyasından düzenlenen assembler, nesne dosyasına dönüştürür ve obhect_file dosyasına kaydeder bu dosyada Header, Text ve End kayıtları biçiminde saklanır. </p>
<h3>Pass2 fonksiyonun içeriği</h3>
  <ul>
    <li>convert_byte fonksiyonu X'F1',C'EOF' formattaki gibi karakterleri hexademical'e çevirmemizi sağlar </li>
    <li>convert_word fonksiyonu Verilen sayısal değeri 6 haneli hexadecimal formata çevirir</li>
    <li>generate_machine_code fonksiyonu opcode ve adresi birleştirerek makine kodu oluşturur.</li>
    <li>write_text_record fonksiyonu Mevcut metin kaydını nesne programına yazar ve yeni bir metin kaydı başlatırız metin kaydının uzunluğ, içindeki makine kodlarının toplam uzunluğuna göre hesaplama işlemi yaparoz</li>
    <li>intermediate_file Dosyası ile ara dosyayı okuma ve object_file dosyasına object programı yazma işlemleri geçrekleştirme işlemlerini yaparız</li>
    <li>Header kaydı ile object programa yazma işlemi gerçeklşetiriz H'program_name ve program uuznluğu bilgisini burada object_file dosyasına yazarız</li>
    <li>Sıradaki işlemler makine koduna dönüştürülmesi işlemleri gerçekletirilir.  </li>
    <li>object_code var ise mevcut metin kaydına makine kodu eklenir eğer mevcut metin kaydının uzunluğu 60 byte'ı aşıyorsa write_text_record fonksiyonu çağrılarak mevcut metin kaydı yazılır ve yeni bir metin kaydı başlatılır.</li>
    <li>text kaydının bitiminde End kaydı başlatılır ve ardından başlangıç adresi yazılır</li>
    <li>bütün kayıtlar object_file dosyasına yazılır</li>
  </ul>
<br>
<br>
<hr>
<H1>Kullanıcı Ara Yüzü</H1>
<hr>
<p>Kullanıcı ara yüzü Tkinter ile oluşturulmuş kod çalıştırıldığında ekranda karşılaşcağınız şu şekildedir</p>
<img>
<p>Input Assembly Code alanında SIC/XE mimarisine ait yazacağınız assemler koda aittir burada save butonuna basarak dosyayı input_file dosyasına kaydetme işlemi gerçekleştirebilirsiniz pass1 butonuna tıklandığında ekran yazdığınız assembler'ın etiket ve adreslerini görebileceğiniz bir text alanı vardır pass2 butonuna tıklandığında oluşan object kod çıktısını oluşmaktadır</p> 
S
