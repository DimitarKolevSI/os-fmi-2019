## Обработка на текст - Седмица 3 и 4

**Зад 1. 03-a-0200**  <br />Сортирайте /etc/passwd лексикографски по поле UserID.

`sort -t : -k 3 /etc/passwd`

**Зад 2. 03-а-0201** <br />Сортирайте /etc/passwd числово по поле UserID. (Открийте разликите с лексикографската сортировка)

`sort -n -t : -k 3 /etc/passwd`

**Зад 3. 03-а-0211** <br />

Изведете само 1-ва и 5-та колона на файла /etc/passwd спрямо разделител ":".

`cut -d : -f 1,5 /etc/passwd`

**Зад 4. 03-а-1500** <br/>

Изведете съдържанието на файла /etc/passwd от 2-ри до 6-ти символ.

`cut -c 2-6 /etc/passwd`

**Зад 5. 03-а-1500** <br />Намерете броя на символите в /etc/passwd. А колко реда има в /etc/passwd?

`wc -c /etc/passwd` пресмята символите <br />`wc -l /etc/passwd` пресмята редовете

**Зад 6. 03-а-2000** <br />

Извадете от файл /etc/passwd:

- първите 12 реда `head -n 12 /etc/passwd`
- първите 26 символа `head -c 26 /etc/passwd`
- всички редове, освен последните 4 `head -n -4 /etc/passwd`
- последните 17 реда `tail -n 17 /etc/passwd`
- 151-я ред `sed -n '159p etc/passwd'`
- последните 4 символа от 13-ти ред `sed -n '13p /etc/passwd | tail -c 5`

**Зад 7. 03-а-2100** <br /> Отпечатайте потребителските имена и техните home директории от /etc/passwd.

`cut -d : -f 1,6 /etc/passwd`

**Зад 8. 03-а-2110**<br/>

Отпечатайте втората колона на /etc/passwd, разделена спрямо символ '/'.

`cut -d / -f 2 /etc/passwd`

**Зад 9. 03-а-3000** <br />Запаметете във файл в своята home директория резултатът от командата ls -l изпълнена за вашата home директорията. <br />Сортирайте създадения файла по второ поле (numeric, alphabetically).

`ls -l | sort -n -k 2 > sortedListAll.txt`

**Зад 10. 03-а-5000**<br/>Отпечатайте 2 реда над вашия ред в /etc/passwd и 3 реда под него // може да стане и без пайпове

`grep 62117 -B 2 -A 3 /etc/passwd`

**Зад 11. 03-а-5001** <br/>Колко хора не се казват Ivan според /etc/passwd

`cat /etc/passwd | grep -v "Ivan " |wc -l`

**Зад 12. 03-а-5002** <br/>Изведете имената на хората с второ име по-дълго от 7 (>7) символа според /etc/passwd

`cut -d : -f 5 /etc/passwd | cut -d ',' -f 1 | cut -d ' ' -f 2 | grep '\([a-zA-Z]\)\{8,\}'`

**Зад 13. 03-а-5003** <br />Изведете имената на хората с второ име по-късо от 8 (<=7) символа според /etc/passwd // !(>7) = ?

`cut -d : -f 5 /etc/passwd | cut -d ',' -f 1 | cut -d ' ' -f 2 | grep '^\([a-zA-Z]\)\{1,7\}$'`

**Зад 14. 03-а-5004** <br/>Изведете целите редове от /etc/passwd за хората от 03-a-5003

`cat /etc/passwd | grep "x:[0-9]\+:[0-9]\+:\([a-zA-Z]\+\s\)\([a-zA-Z]\{1,7\}\),"`

**Зад 15. 03-b-0300** <br/>Намерете факултетния си номер във файлa /etc/passwd.

`cat /etc/passwd | grep "Gyokan Syuleymanov" | cut -c 2-6`

**Зад 16. 03-b-3000** <br/>Запазете само потребителските имена от /etc/passwd във файл users във вашата home директория.

`cut -d : -f 1 /etc/passwd > users.txt`

**Зад 17. 03-b-3450** <br/>Колко коментара има във файла /etc/services ? Коментарите се маркират със символа #, след който всеки символ на реда се счита за коментар.

`cat /etc/services | grep "#\s.*" | wc -l`

**Зад 18. 03-b-3450** <br>Вижте man 5 services. Напишете команда, която ви дава името на протокол с порт естествено число N. Командата да не отпечатва нищо, ако търсения порт не съществува (например при порт 1337). Примерно, ако номера на порта N е 69, командата трябва да отпечати tftp.

`cat /etc/services | grep " 69/" | tr -s [:blank:] | cut -d ' ' -f 1 | uniq`

**Зад 19. 03-b-3500** <br/>Колко файлове в /bin са shell script? (Колко файлове в дадена директория са ASCII text?)

`ls -l /bin | cut -c 1-10 | grep x | wc -l`

**Зад 20. 03-b-3600** <br/>Направете списък с директориите на вашата файлова система, до които нямате достъп. Понеже файловата система може да е много голяма, търсете до 3 нива на дълбочина. А до кои директории имате достъп? Колко на брой са директориите, до които нямате достъп?

`find / -maxdepth 3 -type d -ls | tr -s [:blank:] | grep " d[r]" | cut -d ' ' -f 11` - Директориите до които имам достъп <br/>
`find / -maxdepth 3 -type d -ls | tr -s [:blank:] | grep " d[^r]" | wc -l` - Брой на директроиите до които нямам достъп <br/>

**Зад 21. 03-b-4000** <br />Създайте следната файлова йерархия. <br/>/home/SI/s62117/dir1/file1<br/>/home/SI/s62117/dir1/file2<br/>/home/SI/s62117/dir1/file3<br/>

`touch /home/SI/s62117/dir/file{1,2,3}` 

Посредством vi въведе съдържание. <br />

Изведете на екрана:

* статистика за броя редове, думи и символи за всеки един файл 

`wc -l file{1,2,3}; wc -w file{1,2,3}; wc -m file{1,2,3}`

* статистика за броя редове и символи за всички файлове 

  `cat file{1,2,3} | wc -l; cat file{1,2,3} | wc -w; cat file{1,2,3} | wc -m`

* общия брой редове на трите файла

  `cat file{1,2,3} | wc -l`

**Зад 22. 03-b-4001**<br/>Във file2 подменете всички малки букви с главни.

`ggVGU` - Команда във вим

**Зад 23. 03-b-4002** <br/>Във file3 изтрийте всички "1"-ци.

`:%s/1//g` - Команда във вим

**Зад 24. 03-b-4003**<br/>Изведете статистика за най-често срещаните символи в трите файла.

`cat file{1,2,3} | sort | uniq -c`

**Зад 25. 03-b-4004** <br/>Направете нов файл с име по ваш избор, който е конкатенация от file{1,2,3}. <br/ ><!--Забележка: съществува решение с едно извикване на определена програма - опитайте да решите задачата чрез него.-->

`cat file{1,2,3} > concatenated`

**Зад 26. 03-b-4005** <br />Прочетете текстов файл file1 и направете всички главни букви малки като запишете резултата във file2.

`cat file1 | tr '[:upper:]' '[':lower:']' > file2`

**Зад 27. 03-b-5200**<br/>Изтрийте всички срещания на буквата 'a' (lower case) в /etc/passwd и намерете броят на оставащите символи.

`cat /etc/passwd | sed 's/a//g' | wc -m`

**Зад 28. 03-b-5300**<br/>Намерете броя на уникалните символи, използвани в имената на потребителите от /etc/passwd.

`cut -d : -f 5 /etc/passwd | cut -d ' ' -f 1,2 | cut -d , -f 1 | grep -o . | sort -u | wc -l`

**Зад 29. 03-b-5400**<br/>Отпечатайте всички редове на файла /etc/passwd, които не съдържат символния низ 'ov'.

`cat /etc/passwd | grep -v ov`

**Зад 30. 03-b-6100**<br/>Отпечатайте последната цифра на UID на всички редове между 28-ми и 46-ред в /etc/passwd.

`awk "NR >= 28 && NR <= 46" /etc/passwd | cut -d : -f 3 | grep -o '.\{1\}$'`