Как создать один файл exe из нескольких файлов python pygame с несколькими каталогами активов с помощью pyinstaller на Windows:

Во-первых, установите pyinstaller.

Откройте командную строку Windows, введите:

```
pip install pyinstaller
```

Сделайте игру python. Скажем, основной файл игры называется main_game_script.py, расположенный в

```
C:\Users\USERNAME\Documents\python\game_dir
```

Добавьте эту функцию в main_game_script.py. Обязательно импортируйте ОС и систему. (Я никогда бы сам не понял, что мне нужно добавить эту функцию в свою игру, но она работает, так что спасибо тому, кто опубликовал ее в какой-то другой теме)

```
import sys
import os

def resource_path(relative_path):
    try:
    # PyInstaller creates a temp folder and stores path in _MEIPASS
        base_path = sys._MEIPASS
    except Exception:
        base_path = os.path.abspath(".")

    return os.path.join(base_path, relative_path)
```

Чтобы загрузить изображения в игру, вызовите эту функцию, например:

```
asset_url = resource_path('assets/chars/hero.png')
hero_asset = pygame.image.load(asset_url)
```

Когда ваша игра будет готова к упаковке в EXE, откройте командную строку Windows. Перейдите в основной каталог игры и введите:

```
pyinstaller --onefile main_game_script.py
```

Это будет выглядеть так:

```
C:\Users\USERNAME\Documents\python\game_dir>pyinstaller --onefile main_game_script.py
```

Это создаст четыре важных элемента:

```
- a main_game_script.spec file in the game_dir
- a 'build' dir in the game_dir
- a 'dist' directory in the game_dir
- a main_game_script.exe will be created in the 'dist' directory.
```

Выполнение команды выдает массу предупреждений и журналов. Я не знаю, что все это значит. Но пока конечная строка вывода говорит об успехе, вы, вероятно, хороши. Ваш exe пока не будет работать. Во-первых, вы должны изменить файл .spec (который теперь существует в game_dir), чтобы добавить необходимые пути к игровым активам в exe:

Откройте файл main_game_script.spec в блокноте или что-то еще. Замените пустой список datas[] такими путями к каталогу активов (используя кортежи!):

```
datas=[('assets/chars/*','assets/chars'),('assets/tiles/*.png','assets/tiles'),('assets/fonts/*','assets/fonts')],
```

Первое значение каждого кортежа-это фактические имена файлов, которые вы хотите импортировать. Второе значение-это относительный путь от вас main_game_script.py Синтаксис и пути должны быть идеальными, иначе он не будет работать и может не выдать ошибку

Сохраните и закройте файл "main_game_script.spec". Вернитесь в командную строку windows. Тип:

```
pyinstaller main_game_script.spec
```

[[Python]] [[exe]]

