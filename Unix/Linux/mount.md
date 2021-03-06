<h1>Добавить новый диск в рабочую станцию</h1>

Шаги по созданию нового раздела:
1. Добавить жесткий диск к серверу
2. Убедиться при помощи утилиты fdisk о подключении нового диска ```fdisk -l```
3. Определить диск который необходимо подключить, часто это ```/dev/sdb```,   ```/dev/vdb```
4. Что бы разбить конкретный диск ```fdisk /dev/vdb```
5. После необходимо ввести подкоманду ```n``` она создает раздел
6. На этом шаге необходимо указать номер раздела, при создании нового диска лучше использовать значение по умолчанию  ```p\1```

	<img src="https://blog.sedicomm.com/wp-content/uploads/2018/03/izobrazhenie_2020-12-23_000927.png">

8. Дайте значение первого сектора. Если это новый винт, всегда выбирайте значение по умолчанию. Если вы создаете второй раздел на том же диске, то нужно добавить 1 в последний сектор предыдущего раздела. Укажите значение последнего сектора или размер раздела. Всегда рекомендуется указывать размер раздела. Всегда используйте префикс **_+_**, чтобы избежать ошибки.

 <img src="https://blog.sedicomm.com/wp-content/uploads/2018/03/izobrazhenie_2020-12-23_001054.png">
 Сохраните после и выйдите
 
 9. Теперь отформатируйте диск с помощью команды mkfs. ```mkfs.ext4 /dev/vdb1```
 10. Как только форматирование завершено, теперь монтируйте раздел, как показано ниже. ```mount /dev/vdb1 /место для монтирования```
 11. Сделайте запись в файле /etc/fstab для постоянной установки во время загрузки. ```/dev/vdb1 /data ext4 defaults 0 0```

[[Unix]] [[Linux]] [[Ubuntu]]