# Hands-on Linux-05 : Filters and Control Operators
​
Purpose of the this hands-on training is to teach the students how to use filters and control operators in Linux.
(Bu uygulamalı eğitimin amacı, öğrencilere Linux'ta filtrelerin ve kontrol operatörlerinin nasıl kullanılacağını öğretmektir.)
​
## Learning Outcomes
​
At the end of the this hands-on training, students will be able to;
​
- Use filter commands.
​
- Pipe commands.
​
- Use Control operators.

Bu uygulamalı eğitimin sonunda öğrenciler;
​
- Filtre komutlarını kullanın.
​
- Pipe(Boru) komutları.
​
- Kontrol işleçlerini kullanın.
​
## Outline
​
- Part 1 - Using Filters
​
- Part 2 - Using Control Operators

- Bölüm 1 - Filtreleri Kullanma
​
- Bölüm 2 - Kontrol Operatörlerini Kullanma
​
## Part 1 - Using Filters
​
**cat**

- concatenate files and print on the standard output
​
- Create a folder and name it filters.

- dosyaları birleştirin ve standart çıktıya yazdırın
​
- Bir klasör oluşturun ve filtreler olarak adlandırın.
​
```bash
mkdir filters
cd filters
```
- Create a `text` file named `days.txt`.
- "days.txt" adlı bir "metin" dosyası oluşturun.
​
```bash
vim days.txt
```
​
```bash
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday
```
- Display the content of days.txt.
- days.txt içeriğini görüntüleyin.
```bash
cat days.txt
```
- Show what cat command does when used in a pipe.
- Bir kanalda kullanıldığında cat komutunun ne yaptığını gösterin.
​
```bash
cat days.txt | cat | cat | cat | cat
```
- Create a `text` file named `count.txt`.
- "count.txt" adlı bir "metin" dosyası oluşturun.
​
```bash
nano count.txt
```
```text
one
two
three
four
five
six
seven
eight
nine
ten
eleven 
```
- Display the content of count.txt.
- count.txt içeriğini görüntüleyin.

```bash
cat count.txt
```

**tee**

- Read from standard input and write to standard output and files
​
- Write the content of the count.txt file in reverse order to another file named temp.txt and display the content of temp.txt in reverse order.

- Standart girdiden okuyun ve standart çıktıya ve dosyalara yazın
​
- Count.txt dosyasının içeriğini temp.txt adlı başka bir dosyaya ters sırada yazın ve temp.txt içeriğini ters sırada görüntüleyin.

# tac komutu ters cat demektir. Yani dosya içindeki metni tersten yazdırır.

```bash
tac count.txt | tee temp.txt | tac
```
# tee burada tac'tan gelen ters yazılmıi metni olduğu gibi temp.txt dosyası oluşturarak bunun içine atar. Dolayısıyla bir daha tac yazıldığı zaman tersi ters çevirir. Yani olduğu gibi bir önceki ifadeye çecirmiş oldu.

- Check whether the temp.txt file created and display the content.
​- Temp.txt dosyasının oluşturulup oluşturulmadığını kontrol edin ve içeriği görüntüleyin.

```bash
ls
cat temp.txt
```

**grep**
​
- Print lines that match patterns. The most common use of grep is to filter lines of text containing (or not containing) a certain string.

- Create a `text` file named `tennis.txt`.

- Desenlerle eşleşen çizgileri yazdırın. Grep'in en yaygın kullanımı, belirli bir dize içeren (veya içermeyen) metin satırlarını filtrelemektir.

- "tennis.txt" adlı bir "metin" dosyası oluşturun.
​
```bash
cat > tennis.txt
​
Amelie Mauresmo, Fra
Justine Henin, BEL
Serena Williams, USA
Venus Williams, USA
```
>**press ctrl+d for EOF**
​
- Display the content of tennis.txt.
- Tennis.txt içeriğini görüntüleyin.

```bash
cat tennis.txt
```

- Display only the lines of tennis.txt that includes 'Williams'.
- Sadece 'Williams' içeren tenis.txt satırlarını görüntüleyin.
​
```bash
cat tennis.txt | grep Williams
```
# grep -i williams dersek, büyük ve küçük harf duyarlılığı olmadan williams kelimesini arar.
# grep -w us deseydik bu ifade yazdırmazdı. Çünkü bu şekilde komut girdiğimizde kelime olarak görmek isteriz ve böyle bir ifade metinde yoktur.
# grep -wi usa deseydik, bu ifade yazdırırdı. Çünkü kelime olarak büyük ve küçük harf duyarlılığı olmadan getir demek istemiş oluyoruz.

- Display only the lines of tennis.txt that includes 'us'.
​
```bash
cat tennis.txt | grep us
```

- Display the owners column (3rd column) of all the files in current directory.
​
**cut**

- The cut filter can select columns from files, depending on a delimiter or a count of bytes
- Kesme filtresi, sınırlayıcıya veya bayt sayısına bağlı olarak dosyalardan sütunlar seçebilir
​
​
```bash
ls -l | cut -d' ' -f3
```
# Benim ifadem aralarında boşluklar bulunan sütunlardan ibaret. Bu sütunları da tek tek ele alabilmem için öncelikle bir ayraç vermem lazım. Bu sebeple yukarıdaki komut koşturulmuştur. 

- Display the content of /etc/passwd directory.
- /etc/passwd dizininin içeriğini görüntüleyin.
​
```bash
cat /etc/passwd
```
# kullanıcıları getiren komuttur.

- Display only the usernames.
​- Yalnızca kullanıcı adlarını görüntüleyin.

```bash
cut -d: -f1 /etc/passwd
```
# Pipe yapmadan sadece dosya ismi yazarak kullanımı

**tr**
​
- The command 'tr' stands for 'translate’. It is used to translate, like from lowercase to uppercase and vice versa or new lines into spaces.

- Create a `text` file named `clarusway.txt`.

- 'tr' komutu 'tercüme' anlamına gelir. Küçük harften büyük harfe ve tersi gibi çevirmek veya yeni satırları boşluklara çevirmek için kullanılır.

- "clarusway.txt" adlı bir "metin" dosyası oluşturun.
​
​
```bash
cat << EOF > clarusway.txt
Clarusway:Road to reinvent yourself.
EOF
```

- Display the content of clarusway.txt.
- clarusway.txt içeriğini görüntüleyin.
​
```bash
cat clarusway.txt
```

- In the content of clarusway.txt, replace or translate aer letters with 'QAZ'.
- clarusway.txt içeriğinde aer harflerini 'QAZ' ile değiştirin veya çevirin.
​
```bash
cat clarusway.txt | tr aer QAZ
```
# tr komutu ile sırası ile a yerine Q, e yerine A ve r yerine Z yazdır anlamına gelmektedir.
​
- Write the content of count.txt on the same line.
- Count.txt içeriğini aynı satıra yazın.
​
```bash
cat count.txt | tr '\n' ' '
```
# '\n' işareti ile bu dosyanın sonundaki enterları, yani yeni satır gizli işaretlerinin yerine boşluk getirmesini istiyoruz. 
​
- Delete all the vowels in the content of clarusway.txt.
- clarusway.txt içeriğindeki tüm ünlüleri silin.
​
```bash
cat clarusway.txt | tr -d aeiou
```
​
- Write the whole content of clarusway.txt in capital letters.
- clarusway.txt dosyasının tüm içeriğini büyük harflerle yazın.
​
```bash
cat clarusway.txt | tr [a-z] [A-Z]
```
# Bu ifade ile clarusway.txt dosyasının içindeki tüm küçük harfleri büyük harflere çevirir.

**wc**
​
- Print line, word, and charecters for each file.

- Count the lines, words and letters of the content of count.txt.

- Her dosya için satır, kelime ve karakterleri yazdırın.

- count.txt içeriğindeki satırları, kelimeleri ve harfleri sayın.
​
```bash

wc count.txt
```
# Satırları, kelimeleri ve harfleri bize sırasıyla yazdırır.

- Find how many users are there in the computer.
- Bilgisayarda kaç kullanıcı olduğunu bulun.

```bash
wc -l /etc/passwd
```
# sadece satır sayısını gösterir.
# wc -c count.txt komutu bize sadece karakterlerin sayısını gösterir.

**sort**
​
- The sort filter will default to an alphabetical sort. The sort filter will default to an alphabetical sort.

- Create a `text` file named `marks.txt`.

- Sıralama filtresi, varsayılan olarak alfabetik bir sıralama olacaktır. Sıralama filtresi, varsayılan olarak alfabetik bir sıralama olacaktır.

- "marks.txt" adlı bir "metin" dosyası oluşturun.
​
```bash
cat << EOF > marks.txt
aaron   70
julia   80
albert  90
james   60
kate    60
john    80
oliver  75
tom     54
victor  30
walter  60
jane    100
EOF
```

- Display the content of marks.txt.
-marks.txt içeriğini görüntüleyin.
​
```bash
cat marks.txt
```

- Sort the content of marks.txt.
-marks.txt içeriğini sıralayın.
​
```bash
sort marks.txt
```
# a-z ye sırasıyla dosyaları getirdi.

- Sort the content of marks.txt in reverse order.
- mark.txt içeriğini ters sırada sıralayın.
​
```bash
sort -r marks.txt
```

**uniq**
​
- report or omit repeated lines. With the help of uniq command you can form a sorted list in which every word will occur only once.

- Create a `text` file named `trainees.txt`.

- tekrarlanan satırları bildirin veya atlayın. uniq komutunun yardımıyla, her kelimenin yalnızca bir kez geçeceği sıralı bir liste oluşturabilirsiniz.

- "trainees.txt" adlı bir "metin" dosyası oluşturun.
​
```bash
cat << EOF > trainees.txt
john
james
aaron
oliver
walter
albert
james
john
travis
mike
aaron
thomas
daniel
john
aaron
oliver
mike
john
EOF
```

- Display the content of trainees.txt.
- Trainees.txt içeriğini görüntüleyin.
​
```bash
cat trainees.txt
```

- Display only the unique names in the content of trainees.txt.
​
******before using uniq command, the file must be sorted******

- Trainees.txt içeriğinde yalnızca benzersiz adları görüntüleyin.
​
******uniq komutunu kullanmadan önce dosya sıralanmalıdır******
​
```bash
sort trainees.txt | uniq
```
# uniq komutunu kullandığımızda tekrar eden dosyaları siler ve sort komutu ile birlikte kullandığımız için alfabetik sıra halinde karşımıza çıkarır.

**comm**

- Compare two sorted files line by line. By default, `comm` will always display three columns. 
First column indicates non-matching items of first file, second column indicates non-matching items 
of second file, and third column indicates matching items of both the files. 

- Both the files has to be in sorted order for 'comm' command to be executed.
​
- Create a `text` file named `file1.txt`.
​
- Sıralanmış iki dosyayı satır satır karşılaştırın. Varsayılan olarak, "comm" her zaman üç sütun görüntüler.
İlk sütun, birinci dosyanın eşleşmeyen öğelerini, ikinci sütun eşleşmeyen öğeleri gösterir
ikinci dosyanın ve üçüncü sütun, her iki dosyanın eşleşen öğelerini gösterir.

- 'comm' komutunun çalıştırılabilmesi için her iki dosyanın da sıralanmış olması gerekir.
​
- "file1.txt" adlı bir "metin" dosyası oluşturun.

```bash
cat << EOF > file1.txt
Aaron
Bill
James
John
Oliver
Walter
EOF
```

- Create another `text` file named `file2.txt`.
- "file2.txt" adlı başka bir "metin" dosyası oluşturun.
​
```bash
cat << EOF > file2.txt
Guile
James
John
Raymond
EOF
```

# EOF'nin amacı: Cat komutu ile iki ok işareti yazıp yukarıdaki komutu yazdığımızda file2.txt dosyasının içerisine ifadeleri EOF'yi(ayraçı) görene kadar yaz demektir. EOF olması gerekli bir şey değil yerine herhangi bir isim yazdıradabiliriz.

- Compare file1.txt and file2.txt.
​
******before using comm command, files must be sorted******

- file1.txt ve file2.txt'i karşılaştırın.
​
******com komutunu kullanmadan önce dosyalar sıralanmalıdır******
​
```bash
comm file1.txt file2.txt
```
# ilk sütun file1.txt'de yer alanlar, ikinci sütun file2.txt de yer alanlar,
# üçüncü sütun ise kesişim kümelerinde yer alanları yazdırır.

- EXERCISE:
​
  - Create a file named `countries.csv`.
  "countries.csv" adlı bir dosya oluşturun.

```bash
cat << EOF > countries.csv
Country,Capital,Continent
USA,Washington,North America
France,Paris,Europe
Canada,Ottawa,North America
Germany,Berlin,Europe
EOF
```
  - Cut only 'Continent' column | Remove header | Sort the output | List distinct values | Save it to 'continent.txt' and display on the screen.
  - Yalnızca 'Kıta' sütununu kes | Başlığı kaldır | çıktıyı sırala | Farklı değerleri listeleme | Onu 'continent.txt' dosyasına kaydedin ve ekranda görüntüleyin.
​
```bash
********************************
```
## Part 2 - Using Control Operators
​
>**;**
​
- More than one command can be used in a single line with `;`.

- Write two seperate cat command on the same line using ;.
​
- `;` ile tek satırda birden fazla komut kullanılabilir.

- ; kullanarak aynı satıra iki ayrı cat komutu yazın.
​
```bash
cat days.txt ; cat count.txt 
```

```bash
echo Hello ; echo World! 
```
# Noktalı virgül olumca her iki komutu da birbirinden bağımsız olarak çalıştırır.

>**&**

- When a line ends with an ampersand &, the shell will not wait for the command to finish. You will get your shell prompt back, and the command is executed in background. You will get a message when this command has finished executing in background.
​
- Run sleep 10 command and show that the kernel is busy until the process of this command ends.

- Bir satır & işaretiyle bittiğinde, kabuk komutun bitmesini beklemeyecektir. Kabuk isteminizi geri alacaksınız ve komut arka planda yürütülür. Bu komut arka planda çalışmayı bitirdiğinde bir mesaj alacaksınız.
​
- Sleep 10 komutunu çalıştırın ve bu komutun işlemi bitene kadar çekirdeğin meşgul olduğunu gösterin.
​
```bash
sleep  10
```
# Yeni bir komut çalışabilmem için bana terminalimi geri veriyor ve bu komut arka planda çalışmaya devam ediyor.

- Run sleep 20 command and let this command work behind while you're running other commands.
- Sleep 20 komutunu çalıştırın ve diğer komutları çalıştırırken bu komutun çalışmasına izin verin.
​
```bash
sleep  20 &
ls -l
cat count.txt
cat days.txt
```

>**$?**
​
- This control operator is used to check the status of last executed command. If status shows '0' then command was successfully executed and if shows '1' then command was a failure.

- Run ls command and show that it is executed successfully.

- Bu kontrol operatörü, son çalıştırılan komutun durumunu kontrol etmek için kullanılır. Durum '0' gösteriyorsa, komut başarıyla yürütüldü ve '1' gösteriliyorsa komut başarısız oldu.

- ls komutunu çalıştırın ve başarıyla yürütüldüğünü gösterin.
​
​
```bash
ls
echo $?
```
# Bize son koşturduğumuz komutun sonucunu verir. 0 ise başarılı, 0'dan başka bir rakamsa başarısız demektir.

- Run lss command and show that it failed.
- lss komutunu çalıştırın ve başarısız olduğunu gösterin.
​
```bash
lss
echo $?
```

Exit Code | Meaning |
|:-------:|---------|
|1| Catchall for general errors
|2| Misuse of shell builtins
|126| Command invoked cannot execute
|127| Command not found
|128| Invalid argument to exit
|128+n| Fatal error signal "n"
|255| Exit status out of range (exit takes only integer args in the range 0 - 255)

>**&&**

- The command shell interprets the && as the logical AND. When using this command, the second command will be executed only when the first one has been successfully executed.
​
- Display days.txt and if it runs properly display count.txt.

- Komut kabuğu, &&'yi mantıksal VE olarak yorumlar. Bu komutu kullanırken, ikinci komut yalnızca birincisi başarıyla yürütüldüğünde yürütülür.
​
- days.txt'yi görüntüleyin ve düzgün çalışıyorsa count.txt'yi görüntüleyin.
​
```bash
cat days.txt && cat count.txt
```
# ilk komut çalışıyorsa diğer komut da çalışır. Yani birbirlerine bağlılar. Yani ikinci komut çalışacak bir komut dahi olsa ilki çalışmadığı içinn o da çalışmaz.

- Display days.text and if it runs properly display count.txt.

- days.text'i görüntüleyin ve düzgün çalışıyorsa count.txt'yi görüntüleyin.
​​
```bash
cat days.text && cat count.txt
```

>**||**

- The command shell interprets the (||) as the logical `OR`. This is opposite of logical `AND`. Means second command will execute only when first command will be a failure.
​
- Display days.txt or write 'clarusway' on the screen, then write 'one'.

- Komut kabuğu (||)'yı mantıksal 'VEYA' olarak yorumlar. Bu, mantıksal "VE"nin tersidir. İkinci komutun yalnızca ilk komut başarısız olduğunda yürütüleceği anlamına gelir.
​
- days.txt dosyasını görüntüleyin veya ekrana 'clarusway' yazın, ardından 'one' yazın.
​
```bash
cat days.txt || echo clarusway ; echo one
```
# İlk komut çalışmasa bile ikinci komut çalışır.

- Write 'first' or write 'second' on the screen, then write 'third'.
- Ekrana 'birinci' veya 'ikinci' yazın, ardından 'üçüncü' yazın.
​
```bash
echo first || echo second ; echo third
# ilk komut çalışır, ikinci komut çalışmaz. Echo komutu herhalükarda çalışır.
zecho first || echo second ; echo third
# ilk komut çalışmaz, ikinci komut çalışır. Echo komutu herhalükarda çalışır.
```

>**&& and ||**

# if else yapısını bu komutlar ile yapabiliyoruz.

- We can use this logical AND and logical OR to write an if-then-else structure on the command line. This example uses echo to display whether the rm command was successful.
​
- Make a copy of file1.txt and named it file11.txt.

- Komut satırında bir if-then-else yapısı yazmak için bu mantıksal AND ve mantıksal OR'yi kullanabiliriz. Bu örnek, rm komutunun başarılı olup olmadığını görüntülemek için yankıyı kullanır.
​
- file1.txt dosyasının bir kopyasını oluşturun ve file11.txt olarak adlandırın.
​
```bash
cp file1.txt file11.txt
```
- Delete file11.txt and write a message if it is deleted properly.
- file11.txt dosyasını silin ve düzgün silinmişse bir mesaj yazın.
​
```bash
rm file11.txt && echo 'it worked' || echo 'it failed'
```
# Önce file1.txt komutu olduğu için silebiliriz. Dolayısıyla ilk komut çalışır. aralarında && komutu olması sebebi ile ilk komut çalıştığı için ikincisi de çalışır. || komutu kendisinden önceki ifadeyi bir bütün olarak görüyor. Dolayısıyla kendinden önceki ifade çalıştığı için echo "it failed" komutu çalışmayacak. Bu komutu çalıştırdıktan sonra bir daha aynı komutu çalıştırmaya kalkarsam file11.txt dosyası silindiği için || komutundan önceki kısım çalışmayacağı için echo "ıt failed" komutu çalışır. Aşağıdaki örnekte bu durum söz konusudur.

- Run the last command again.
- Son komutu tekrar çalıştırın.
​
​```bash
rm file11.txt && echo 'it worked' || echo 'it failed'
```

>**#**

- Everything written after a pound sign (#) is ignored by the shell. This is useful to write a shell comment but has no influence on the command execution or shell expansion.​

- Run the echo command and add a comment line.
​
- Pound işaretinden (#) sonra yazılan her şey kabuk tarafından dikkate alınmaz. Bu, bir kabuk yorumu yazmak için kullanışlıdır ancak komut yürütme veya kabuk genişletme üzerinde hiçbir etkisi yoktur.​

- echo komutunu çalıştırın ve bir yorum satırı ekleyin.

```bash
echo '# is the comment sign' # echo command displays the string comes after it
# Yorum satırı olduğu için o kısım gözükmez.
echo # is the comment sign

echo \# is the comment sign
# böyle olduğu zaman \ bu işaret # işaretinin gücünü elinden aldığı için çalışır.
```

>** \ **

- Lines ending in a backslash are continued on the next line. The shell does not interpret the newline character and will wait on shell expansion and execution of the command line until a newline without backslash is encountered.

- Escaping characters are used to enable the use of control characters in the shell expansion but without interpreting it by the shell.
​
- Run a single command on multipe lines.

- Ters eğik çizgi ile biten satırlar bir sonraki satırda devam eder. Kabuk, yeni satır karakterini yorumlamaz ve ters eğik çizgi olmayan bir yeni satırla karşılaşılıncaya kadar kabuk genişletmesini ve komut satırının yürütülmesini bekler.

- Kaçan karakterler, kabuk genişletmede kontrol karakterlerinin kabuk tarafından yorumlanmadan kullanılmasını sağlamak için kullanılır.
​
- Birden çok satırda tek bir komut çalıştırın.
​
```bash
echo this command is written \
not only on a single line \
but also on multiple lines.
```
# \ Bu ifadeyi kullandığımız zaman dosyanın sonunda bulunan yeni satır ifadesinin bir nevi gücünü elinden alıyoruz. Görülmediği için komut tek satırla devam ediyor gibi boşluk veriyor. yeni satırı disable etmiş oluyor.

- Write the following sentence on the screen: The special characters are *, \, ", #, $, '.
- Ekrana şu cümleyi yazın: Özel karakterler *, \, ", #, $, ' şeklindedir.
​
```bash
echo The special characters are \*, \\, \", \#, \$, \'.
```
# Yani \ bu işareti koyduğumuzda karakterlerin özel gücü elinden alınmış oluyor.

- EXERCISE:
​
  1.a. Search for “clarusway.doc” in the current directory
    b. If it exists display its content
    c. If it does not exist print message “Too early!”
  2.Create a file named “clarusway.doc” that contains “Congratulations”
  3.Repeat Step 1
​
1 A. Geçerli dizinde "clarusway.doc" dosyasını arayın
    b. Varsa içeriğini göster
    c. Mevcut değilse, “Çok erken!” mesajını yazdırın.
  2. “Tebrikler” içeren “clarusway.doc” adlı bir dosya oluşturun.
  3. Adım 1'i tekrarlayın
  
```bash
********************************
```