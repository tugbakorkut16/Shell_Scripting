# Hands-on Linux-10 : sed & awk command and crontab

Purpose of the this hands-on training is to teach the students how to use sed & awk command and crontab.
Bu uygulamalı eğitimin amacı, öğrencilere sed & awk komutunu ve crontab'ı nasıl kullanacaklarını öğretmektir.

## Learning Outcomes

At the end of the this hands-on training, students will be able to;

- use sed & awk command and crontab.

Bu uygulamalı eğitimin sonunda öğrenciler;

- sed & awk komutunu ve crontab'ı kullanın.

## Outline

- Part 1 - sed command

- Part 2 - awk command

- Part 3 - crontab

- Bölüm 1 - sed komutu

- Bölüm 2 - awk komutu

- Bölüm 3 - crontab

## Part 1 - sed command

- Sed is a stream editor. A stream editor is used to perform a lot of function on a file like searching, find and replace, insertion or deletion.

- Create a folder and name it `sed-awk-command`.

- Sed bir yayın düzenleyicisidir. Bir akış düzenleyici, bir dosya üzerinde arama, bulma ve değiştirme, ekleme veya silme gibi birçok işlevi gerçekleştirmek için kullanılır.

- Bir klasör oluşturun ve "sed-awk-command" olarak adlandırın.

```bash
mkdir sed-awk-command && cd sed-awk-command
```

- Create a file named `sed.txt`. 

```txt
Linux is an OS. Linux is life. Linux is a concept.
I like linux. You like linux. Everyone likes linux.
Linux is free. Linux is good. Linux is hope.
```

### Replacing or substituting string (Dizeyi değiştirme veya ikame etme)

The following sed command replaces the word “linux” with “ubuntu” in the file.
Aşağıdaki sed komutu, dosyadaki “linux” kelimesini “ubuntu” ile değiştirir.

```bash
sed 's/linux/ubuntu/' sed.txt
```
# sedde ilk amacımız linux  ifadesini ubuntu kelimesi ile değiştirmek. sedde aksi durum belirtmediğimiz sürece ilk gördüğü linux isimli kelimeyi ubuntuya çevirir diğer linux yazılı kelimeler aynı kalır.

- `s` specifies the substitution operation. 
- The `/` are delimiters. 
- The `linux` is the search pattern and the `ubuntu` is the replacement string.

- `s`, değiştirme işlemini belirtir.
- `/` sınırlayıcılardır.
- "Linux", arama modelidir ve "ubuntu", değiştirme dizesidir.

**Output:**
```bash
Linux is an OS. Linux is life. Linux is a concept.
I like unutu. You like linux. Everyone likes linux.
Linux is free. Linux is good. Linux is hope.
```
> Pay attention that, by default, the sed command replaces the `first occurrence` of the pattern in each line.
> Varsayılan olarak, sed komutunun her satırdaki örüntünün "ilk oluşumunu" değiştirdiğine dikkat edin.

### 

### Replacing the any occurrence of a pattern in a line (Bir satırdaki herhangi bir desen oluşumunu değiştirme)
Use the /1, /2 etc flags to replace the first, second occurrence of a pattern in a line. The following command replaces the third occurrence of the word “linux” with “ubuntu” in a line.

Bir satırdaki bir kalıbın ilk, ikinci oluşumunu değiştirmek için /1, /2 vb. işaretlerini kullanın. Aşağıdaki komut, bir satırdaki “linux” kelimesinin üçüncü geçişini “ubuntu” ile değiştirir.

```bash
sed 's/linux/ubuntu/3' sed.txt
```
# Bu şekilde komut girdiğiizde 3. linux ifadesindeki kelimeyi ubuntu olarak değiştir demektir.

**Output:**
```bash
Linux is an OS. Linux is life. Linux is a concept.
I like linux. You like linux. Everyone likes ubuntu.
Linux is free. Linux is good. Linux is hope.
```

### Replacing a string by ignoring case distinctions. (Büyük/küçük harf ayrımlarını yok sayarak bir dizeyi değiştirme.)

By, default sed command do not ignore case distinctions. For this `i` pattern can be used.
Varsayılan olarak, sed komutu büyük/küçük harf ayrımlarını göz ardı etmez. Bunun için `i` kalıbı kullanılabilir.

```bash
sed 's/linux/ubuntu/i' sed.txt
```
# Burada ilk karşılaştığı linux kelimesi büyük harf küçük harf duyarlılığı olmaksızın ubuntu kelimesi ile değişir.

**Output:**
```bash
ubuntu is an OS. Linux is life. Linux is a concept.
I like ubuntu. You like linux. Everyone likes linux.
ubuntu is free. Linux is good. Linux is hope.
```

#### Replacing all the occurrence of the pattern in a line (Bir satırdaki desenin tüm oluşumunu değiştirme)

`g flag` (global replacement) defines the sed command to replace all the occurrences of the string in the line.
"g flag" (genel değiştirme), dizenin satırdaki tüm oluşumlarını değiştirmek için sed komutunu tanımlar.

```bash
sed 's/linux/ubuntu/g' sed.txt
```
# Burada tüm linux kelimelerini ubuntu yap diyoruz.

**Output:**
```bash
Linux is an OS. Linux is life. Linux is a concept.
I like ubuntu. You like ubuntu. Everyone likes ubuntu.
Linux is free. Linux is good. Linux is hope.
```

- We can do the same by ignoring case distinctions. Use the combination of `/i` and `/g`.
- Aynısını vaka ayrımlarını göz ardı ederek de yapabiliriz. "/i" ve "/g" birleşimini kullanın.

```bash
sed 's/linux/ubuntu/ig' sed.txt
```
# Burada büyük harf küçük harf ayrımı yapmaksızın tüm linux kelimelerini ubuntu olarak değiştiriyoruz.

**Output:**
```bash
ubuntu is an OS. ubuntu is life. ubuntu is a concept.
I like ubuntu. You like ubuntu. Everyone likes ubuntu.
ubuntu is free. ubuntu is good. ubuntu is hope.
```

#### Replacing from any occurrence to all occurrences in a line (Bir satırdaki herhangi bir oluşumdan tüm oluşumlara değiştirme)

We can replace all the patterns from the any occurrence of a pattern in a line by using the combination of /1, /2 etc and /g. The sed command below replaces the second, third, and so on “linux” word with “ubuntu” word in a line.

/1, /2 etc ve /g kombinasyonunu kullanarak bir satırdaki herhangi bir modelin tüm kalıplarını değiştirebiliriz. Aşağıdaki sed komutu, bir satırdaki ikinci, üçüncü vb. “linux” kelimesini “ubuntu” kelimesi ile değiştirir.

```bash
sed 's/linux/ubuntu/2ig' sed.txt
```
# Her satırda 2. bulduğundaki linuxi büyük harf ve küçük harf duyarlılığı olmaksızın ubuntu kelimesi olarak değiştirir. 

**Output:**
```bash
Linux is an OS. ubuntu is life. ubuntu is a concept.
I like linux. You like ubuntu. Everyone likes ubuntu.
Linux is free. ubuntu is good. ubuntu is hope.
```

#### Replacing string on a specific line number (Dizeyi belirli bir satır numarasıyla değiştirme)

We can limit the sed command to replace the string on a specific line number. The following command only replaces the second line.
Dizeyi belirli bir satır numarasıyla değiştirmek için sed komutunu sınırlayabiliriz. Aşağıdaki komut yalnızca ikinci satırın yerini alır.

```bash
sed '2 s/linux/ubuntu/ig' sed.txt
```
# Satır sayını belirterek bu değişikliği yapabiliriz. 2. satırdaki linuxi büyük harf ve küçük harf duyarlılığı olmaksızın ubuntu kelimesi olarak değiştirir.

**Output:**
```bash
Linux is an OS. Linux is life. Linux is a concept.
I like ubuntu. You like ubuntu. Everyone likes ubuntu.
Linux is free. Linux is good. Linux is hope.
```

## Part 2 - awk command

- Awk is a text pattern scanning and processing language, created by Aho, Weinberger & Kernighan (hence
the name). It searches one or more files to see if they contain lines that matches with the specified patterns and then performs the associated actions. 

- While the sed program works well with character-based processing, the awk program works well with delimited field processing.

- Create a file named `awk.txt`. 

- Awk, Aho, Weinberger & Kernighan tarafından oluşturulan bir metin deseni tarama ve işleme dilidir (dolayısıyla
isim). Belirtilen kalıplarla eşleşen satırlar içerip içermediklerini görmek için bir veya daha fazla dosyayı arar ve ardından ilişkili eylemleri gerçekleştirir.

- sed programı karakter tabanlı işlemede iyi çalışırken, awk programı sınırlandırılmış alan işlemede iyi çalışır.

# Avk komutu sütün olarak ifade edilen tesxtlerde iyi çalışır.

- `awk.txt` adlı bir dosya oluşturun.

```txt
This is line 1
This is line 2
This is line 3
This is line 4
This is line 5
```

### Syntax of awk command

> awk options 'selection _criteria {action }' file

- By default Awk prints every line of data from the specified file.

> awk options 'section _criteria {action }' dosyası

- Varsayılan olarak Awk, belirtilen dosyadaki her veri satırını yazdırır.

```bash
awk '{print}' awk.txt
```
# awk komutunu koştururken süslü parantez içine fonksiyon yazıyorum. Print yazdığımız için awk.txt dosyasının içindeki verileri yazdırır.

**Output:**
```bash
This is line 1
This is line 2
This is line 3
This is line 4
This is line 5
```

### Print the lines which matches with the given pattern
### Verilen desenle eşleşen satırları yazdır

```bash
awk '/This/ {print}' awk.txt
```
# İçerisinde This  geçen satırları yazdırır sadece.

**Output:**
```bash
This is line 1
This is line 2
This is line 3
This is line 4
This is line 5
```

### Splitting a Line Into Fields (Çizgiyi Alanlara Bölme)

By default, the awk command splits the record delimited by a whitespace character.  Awk assigns some variables for each data field as below:
Varsayılan olarak awk komutu, bir boşluk karakteriyle ayrılmış kaydı böler. Awk, her veri alanı için aşağıdaki gibi bazı değişkenler atar:

$0 for the whole line.
$1 for the first field.
$2 for the second field.
$n for the nth field.

```bash
awk '{print $2}' awk.txt
```
# İkinci sütunu yazdırır.

**Output:**
```bash
is
is
is
is
is
```

We can display more field. The example below only display two field.
Daha fazla alan gösterebiliriz. Aşağıdaki örnekte yalnızca iki alan görüntülenir.

```bash
awk '{print $2,$4}' awk.txt
```
# 2 ve 4. sütunları yazdırır.

**Output:**
```bash
is 1
is 2
is 3
is 4
is 5
```

- We can change delimiter by using –F option. First, update the awk.txt as below.
- Sınırlayıcıyı –F seçeneğini kullanarak değiştirebiliriz. Öncelikle awk.txt dosyasını aşağıdaki gibi güncelleyin.

```txt
This is part 1 of line 1 : This is part 2 of line 1
This is part 1 of line 2 : This is part 2 of line 2
This is part 1 of line 3 : This is part 2 of line 3
This is part 1 of line 4 : This is part 2 of line 4
This is part 1 of line 5 : This is part 2 of line 5
```

- Let's separate the fields by `:`.

```bash
awk -F: '{print $2}' awk.txt
```
# Normalde awk komutu bir şey girmediğimiz zaman boşluğu sütunların ayracı olarak görür. İki noktayı(:) ayraç olarak görmesini istersek yukarıdaki komutu koşarız. Yukarıdaki komutun anlamı şimdi ele alınacak dosyayı iki sütun olarak düşünün ve bu iki sütün iki nokta aracılığıyla birbirinden ayrılmış demektir.

**Output:**
```bash
 This is part 2 of line 1
 This is part 2 of line 2
 This is part 2 of line 3
 This is part 2 of line 4
 This is part 2 of line 5
```

- We can use awk command as filter. 
- Filtre olarak awk komutunu kullanabiliriz.

```bash
ls -l | awk '{print $9}'
```

**Output:**
```bash
awk.txt
sed.txt
```

- We can find any string in any specific column. 

```bash
awk '{ if($7 == "3") print $0;}' awk.txt
```
# 7. bölümün 3'e eşit olduğu yeri alın ve bunun sıfırıncısını yazdırın. yani satırın tamamını yazdır demektir.

**Output:**
```bash
This is part 1 of line 3 : This is part 2 of line 3
```

## Part 3 - crontab

- Crontab, stands for `cron table`, which is a list of commands scheduled to run at regular time intervals on the system. 

- If we need to schedule any task on Linux, we should basically edit the crontab file. We can do that using the below command.

- Crontab, sistemde düzenli zaman aralıklarında çalışacak şekilde programlanmış komutların bir listesi olan "cron tablosu" anlamına gelir.

- Eğer Linux üzerinde herhangi bir görev programlamamız gerekirse, temel olarak crontab dosyasını düzenlememiz gerekir. Aşağıdaki komutu kullanarak bunu yapabiliriz.

# crontabtaki amaç, 7/24 çalışan serverımız var ve bu servera uyanıp komut çalıştırmak istemiyoruz ya da düzenli aralıklarla çalıştırmak istediğimiz bir komut var ve bu durumlar için kullanılır. Özellikle Devops tarafında kullanacağız. Otomasyon işlemlerinde.

```bash
crontab -e              # edit the crontab file
# bir tane dosya açıyor
crontab -l              # list current cron tasks
# verilmiş olan emirleri listeliyor.
crontab -u username -e  # edit other users's crontab file
# bir kullanıcı adı vererek o kullanıcının cron(otomasyon) dosyasını editleyebiliyoruz.
```
# Cron ne işe yarar? bir komutu sisteme belli aralıklarla işliyor. 

- Editing the crontab file is not complex, but we should first learn how to set a date and time using 5 * on that file. There are six fields that we use on every cron task line. Those are explained in detail in the below picture.

- crontab dosyasını düzenlemek karmaşık değildir, ancak önce o dosyada 5 * kullanarak tarih ve saat ayarlamayı öğrenmeliyiz. Her cron görev satırında kullandığımız altı alan vardır. Bunlar aşağıdaki resimde ayrıntılı olarak açıklanmıştır.

![crontab format](./crontab-format.png)

- Let’s see few examples;

```bash
* * * * * <shell command>   # execute cron job every minute
# 5 yıldız olduğunda bu her dakika demektir.
0 1 * * * <shell command>   # execute cron job every day at 1 a.m.
# Her gün gece 01.00'da
* * 1 * * <shell command>   # execute every minute in January
# Her Ocak ayı
* * * * 6 <shell command>   # execute every minute on every saturday
# Her cumartesi
0 1/15 * jan,jun mon,fri <command> # execute at every 1 a.m. and 3
                                     p.m. every monday and friday on
                                     january and june
```

- We can also use some regular expressions to define the date part.
- Tarih bölümünü tanımlamak için bazı düzenli ifadeler de kullanabiliriz.

```bash
* = Any/All values           # e.g. *
- = Range of values          # e.g. 1-5 
, = Multiple/List of values  # e.g. 1,2,3
/ = Step values              # e.g. 1/3
```

- Finally let’s create some crontab tasks. Create a cron task writes the system date information every day at 1 p.m. to the date.log file.
- Son olarak bazı crontab görevleri oluşturalım. Bir cron görevi oluştur, sistem tarih bilgilerini her gün saat 1'de yazar. date.log dosyasına.

```bash
crontab -e
0 13 * * * date >> /home/ec2-user/date.log
```

- Create a cron task updates and upgrades our server every Sunday at 3 a.m.
- Bir cron görevi oluşturun, sunucumuzu her Pazar saat 3'te günceller ve yükseltir.

```bash
0 3 * * sun sudo yum update -y
```

-  List the cron tasks.
- Cron görevlerini listeleyin.

```bash
crontab -l
```