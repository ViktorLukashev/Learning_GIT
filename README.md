# Learning_GIT
## Command line

#### Создать файл
```touch %ИМЯ_ФАЙЛА%```

#### Создания директорий
```mkdir %ИМЯ_Папки%```

>С помощью флага `-p` можно создать целую структуру директорий одной командой: `mkdir -p`.

#### Копирование файлов — cp
```
$ cp что_копируем куда_копируем

$ cp index.html /src
# скопировали index.html в папку src
```

Можно указать сразу несколько файлов.

```
$ cp что_копируем что_копируем что_копируем куда_копируем

$ cp index.html style.css script.js /src
# скопировали три файла (index.html, style.css и script.js) в папку src
```

#### Перемещение файлов и папок — mv
```
$ mv table.csv ./very-important-files
# сначала указываем имя файла, который хотим переместить, потом путь — куда перемещаем 

$ cd very-important-files
$ ls
table.csv 
# перешли в папку very-important-files и проверили, что всё сработало
```


Чтение файлов — `cat`

Удаление файлов и папок — `rm`, `rmdir`, `rm -r`

## Эффективная работа с командной строкой
Выполняйте сразу несколько команд. Для этого их нужно разделить двумя амперсандами (`&&`).
пример:
```
$ mkdir second-project && cd second-project && touch index.html style.css
# создаём папку second-project,
# переходим в папку second-project
# и создаём в ней два файла: index.html и style.css
```

«Разгитить» папку, если что-то пошло не так, — `rm -rf .git`

>Разберём подробнее, что такое -rf:
* ключ `-r` (от англ. recursive — «рекурсивно») позволяет удалять папки вместе с их содержимым;
* ключ `-f` (от англ. force — «заставить») избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?».

## Подготовить файлы к сохранению — git add
* Команда `git add` позволяет подготовить файл к сохранению.
* Команда `git add --all` подготовит к сохранению сразу все файлы.
* С помощью `git add` . можно добавить в репозиторий текущую папку со всеми файлами.

## Выполнить коммит — git commit
```$ git commit -m "Мой первый коммит!"```

* Ключ -m позволяет присвоить коммиту сообщение.

## Просмотреть историю коммитов — git log

## Привязываем SSH-ключ к GitHub

1. После выполнения команды ssh-keygen из предыдущего урока в директории ~/.ssh будет создано два файла — id_ed25519 и id_ed25519.pub (или id_rsa и id_rsa.pub — в зависимости от того, какой алгоритм вы использовали):
* id_ed25519/id_rsa — приватный ключ (файл без .pub в конце). Ни в коем случае не копируйте его и не делитесь им.
* id_ed25519.pub/id_rsa.pub — публичный ключ (на это указывает расширение .pub).
  Скопируйте содержимое файла с публичным ключом в буфер обмена.

**macOS**
```
# скопировать содержимое ключа в буфер обмена:
$ pbcopy < ~/.ssh/id_rsa.pub
# для ed25519:
$ pbcopy < ~/.ssh/id_ed25519.pub
```
**Windows**
```
# скопировать содержимое ключа в буфер обмена:
$ clip < ~/.ssh/id_rsa.pub
# для ed25519:
$ clip < ~/.ssh/id_ed25519.pub
```

2. Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта.

3. В меню слева нажмите на пункт SSH and GPG keys.

4. В открывшейся вкладке выберите New SSH key (англ. «новый SSH-ключ»).

5. В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).

6. В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).

7. В поле Key скопируйте ваш ключ из буфера обмена.

8. Нажмите на кнопку Add SSH key (англ. «добавить SSH-ключ»).

9. Проверьте правильность ключа с помощью следующей команды. ```ssh -T git@github.com.```
   Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение.
```
The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.

Вы можете проверить ключи GitHub по [ссылке](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints).

## Привязать удалённый репозиторий к локальному — `git remote add`

Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL. Кнопка справа позволит сделать это мгновенно.

Откройте консоль, перейдите в каталог локального репозитория и введите команду `git remote add` (от англ. remote — «удалённый» и add — «добавить»).
```
$ cd ~/dev/first-project
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
```

`origin` (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). Это значительно упрощает работу.

### Убедиться, что репозитории связаны, — `git remote -v`
```
$ git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)
```
Флаг `-v` — короткая форма флага `--verbose` (англ. «подробный»). Он позволяет показать больше информации в выводе.

## Синхронизируем локальный и удалённый репозитории

### Отправить изменения на удалённый репозиторий — `git push`
```
git push -u origin main
```
В дальнейшем при работе с удалённым репозиторием флаг `-u` можно опустить и писать просто `git push`.

## Хеш — идентификатор коммита - `git log`
**Хеширование** (от англ. hash, «рубить», «крошить», «мешанина») — это способ преобразовать набор данных и получить их «отпечаток» (англ. fingerprint).
Все хеши и таблицу `хеш → информация о коммите` Git сохраняет в служебные файлы. Они находятся в скрытой папке `.git` в репозитории проекта.

### Получить сокращённый лог — `git log --oneline`

## Файл HEAD
>Файл `HEAD` (англ. «голова», «головной») — один из служебных файлов папки `.git`. Он указывает на коммит, который сделан последним (то есть на самый новый).

## Статусы `untracked`/ `tracked`, `staged` и `modified`
Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.
* `untracked` (англ. «неотслеживаемый»)
* `staged` (англ. «подготовленный»)
* `tracked` (англ. «отслеживаемый»)
* `modified` (англ. «изменённый»)

