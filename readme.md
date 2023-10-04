# Шпаргалка по курсу GIT от Яндекс  


## 1. Основы работы с Терминалом:  

**pwd** - узнать пусть к текущей дир-и;  
**cd** ~  - перейти в домашнюю дир-ю;  
**cd ..** - вернуться в родительскую дир-ю;  
**cd _название /след папка_** - переместиться сразу к след. папке;  
**ls** - вывести содержимое дир-и;  
**ls -a** - показать скрытые файлы;  
**ls** ~  - показать содержимое родительской дир-и;  
**touch/mkdir** - создать файл или дир-ю;  
**mkdir -p _dir1/dir-inside/die-deeper_** - создать структуру дир-й;  
**cp _что копируем куда_** - копирование;  
**cp _что копируем что копируем что копируем куда_** - копирование нескольких файлов;  
**mv** - перемещение;  
**cat** - прочитать файл в консоль;  
**rm, rmdir, rm -r** - удалить файл, папку, папку с файлами;  
**mk dir second-project && cd second-project && touch index.html style.css** - выполнить сразу несколько команд;  
**echo "Вторая строка файла" >> file.txt** - допишет новую строку в конец файла;  
**echo "Новая строка" > file.txt** - сотрёт содержимое файла, то есть перезапишет файл целиком.  
Выйти из редактора Vim: нажать Esc, ввести :qa!, нажать Enter;  
**chmod +x имя файла.sh** - эта команда сделает файл исполняемым;  
**./имя файла.sh** - эта команда исполнит скрипт;  


## 2. Основы Git:  

**git config --global user.name "_____"**   
**git config --global user.email _____** - заносим информацию о пользователе в Git, имя и почта;  

_Все настройки хранятся в .gitconfig в домашней дир-ии._  

**cat ~/.gitconfig** или **git config --list** - вывести содержимое файла конфигурации;  
**git init** - сделать папку реп-ем;  
**rm -rf .git** - _разгитить_ папку;  
**git status** - состояние реп-я;  
**git add --all** - добавить все файлы;  
**git add .** - добавить всю папку целиком;  
**git commit -m "____"** - сохранить, зафиксировать изменения;  
**git log** - история коммитов.    

## 3. Работа с SSH ключем:  

**cd** ~ - перейти в домашнюю дир-ю;  
**ls -la .ssh/** - вывести список ключей (если они есть);  
**ssh-keygen -t ed25519 -C "эл. почта"** или **ssh-keygen -t rsa -b 4096 -C "эл. почта"** - генерация SSH пары;  
**ls -a ~/.ssh** или **ls -la ~/.ssh** - посмотреть пару ssh ключей;  

**clip < ~/.ssh/id_ed25519.pub** или **clip < ~/.ssh/id_rsa.pub** - копируем содержимое в буфер;  
**cat ~/.ssh/id_ed25519.pub** или **cat ~/.ssh/id_rsa.pub** - показать в терминале, что б скопировать в ручную;  
**ssh -T git@gitgub.com** - проверить ключ;  


**git remote add origin <ssh ссылка с github>** - привязка удаленного реп-я к локальному;  
_origin_ - имя(псевдоним) удаленного репозитория  
**git remote -v** - проверить, что реп-ии связаны;  
**git push -u origin main(master)** - отправка изменений в удаленный реп-й.  
Первый раз нужно делать с флагом -u. Он связывает одноименный локальный и удаленный реп-ий.  
**git push --set-upstream origin HEAD**. Флаг **--set-upstream** — это «полная», или «длинная», версия флага **-u**.  
А **HEAD** здесь — это синоним текущей ветки.  
С тем же результатом можно было бы выполнить команду **git push -u origin название ветки**.

## 4. Хеш — идентификатор коммита  

_Git хранит таблицу соответствий хеш → информация о коммите. Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. Можно сказать, что хеш — основной идентификатор коммита._  
**git log** - появляется список коммитов.  
**git log --oneline** - автоматически подбирает такую длину сокращённых хешей, чтобы они были уникальными в пределах репозитория и Git всегда мог понять, о каком коммите идёт речь.  

## 5. HEAD — всему голова  

При вызове команды **git log** вы также могли заметить надпись (**HEAD -> master**).  
Файл **HEAD (англ. «голова», «головной»)** — один из служебных файлов папки **.git**  

## 6. С татусы файлов в Git  

Статусы **untracked/tracked**, **staged** и **modified**.  

Статусом **untracked** помечается файл, о существовании которого Git знает, но не следит за изменениями в нём.  
Этот статус — противоположность **tracked**, в который попадают все файлы, отслеживаемые Git.  
Файл переходит в статус **staged** после выполнения **git add**.  
Статус **modified** означает, что файл был изменён.  
Большинство файлов в проектах «шагает» по следующему циклу: «изменён» → «добавлен в список на коммит» → «закоммичен» → «изменён» → и так далее.  

Команда **git status** всегда подскажет, что происходит с файлом: например, он добавлен в список «на коммит» или ещё вообще не отслеживается, или изменён.  

**git status** показывает явно следующие состояния файлов: **untracked, staged** и **modified**.  
**git status** подсказывает, какие команды можно выполнить, чтобы поменять состояние файла.  

## 7. Оформление сообщений к коммитам  

### Корпоративный  
В корпоративном стиле в начале сообщения обычно указывают Jira-ID, а после — текст сообщения.  

$ **git commit -m "LGS-239: Дополнить список пасхалок новыми числами"**  

### Conventional Commits  
Conventional Commits предлагает такой формат коммита: <type>: <сообщение>. Первая часть type — это тип изменений. Таких типов достаточно много. Вот два примера:  

**feat** (сокращение от англ. feature) — для новой функциональности;  
**fix** (от англ. «исправить», «устранить») — для исправленных ошибок.  

**git commit -m "feat: добавить подсчёт суммы заказов за неделю"**  

### GitHub-стиль  
GitHub можно использовать не только для хранения файлов проекта, но и для ведения списка задач (англ. issue) этого проекта.  
Если коммит «закрывает» или «решает» какую-то задачу, то в его сообщении удобно указывать ссылку на неё.  

**$ git commit -m "Исправить #334, добавить график температуры"**  

## 8. Как исправить коммит  

**git commit --amend --no-edit** - дополнить коммит новыми файлами;  
С опцией **--amend** команда **commit** не создаст новый коммит, а дополнит последний.  

**git commit --amend -m "Новое сообщение"** - изменить сообщение коммита.  

**--amend** рассчитан на работу с последним коммитом **(HEAD)**.  

## 9. Как откатиться назад, если «всё сломалось»  

**git restore --staged <file>** - выполнить **unstage** изменений, переведёт файл из **staged** обратно в **modified** или **untracked**;  
**git reset --hard <commit hash>** - «откатит» историю до коммита с хешем **<hash>**. Более поздние коммиты потеряются!;  
**git restore <file>** - откатить изменения, которые не попали ни в **staging**, ни в коммит. «Откатит» изменения в файле до последней сохранённой (в коммите или в staging) версии;  
Может быть так, что вы случайно изменили файл, который не планировали.  
Теперь он отображается в **Changes not staged for commit (modified**. Чтобы вернуть всё «как было», можно выполнить команду **git restore <file>**.  
Изменения в файле «откатятся» до последней версии, которая была сохранена через **git commit** или **git add**.  

## 10. Просматриваем изменения в файлах  
 
**git diff** - сравнит последнюю закоммиченную версию файла с той, что находится в состоянии **modified**;  
**git diff --staged** - покажет изменения в **staged-файлах** относительно последних закоммиченных версий.  

### Сопоставляем коммиты  

**git diff <предыдущий коммит> <следующий коммит>** - сравнивать изменения в двух коммитах; 
По сути команда **git diff A B** выводит список инструкций: как превратить состояние A в состояние B.  
Если поменять A и B местами (**git diff B A**), то и инструкции будут обратные: как превратить B в A. При этом все зелёные строки станут красными, и наоборот.
Попробуйте **git diff <конец> <начало>**. Вместо <конец> можно также передать **HEAD**.  

## 11. Игнорирование файлов в Git  

Чтобы Git игнорировал такие файлы и не пытался добавить их в репозиторий, нужно создать файл **.gitignore**  
Правила из **.gitignore** применяются только к новым (**untracked**) файлам. Если файл уже попал в **staging area** или в коммит, то правила на него не распространяются.  
Сам файл **.gitignore** — это обычный файл в репозитории. Его тоже стоит закоммитить.  

### Комментарий  
\# вот так можно писать комментарии;  
\# они ничего не значат для **.gitignore**,  
\# но они могут быть полезны, чтобы понять, зачем было добавлено то или иное правило.  

### Просто название файла  
Допустим, нужно, чтобы Git игнорировал все файлы **.DS_Store**. Для этого достаточно добавить в **.gitignore** строку с названием файла:  

для macOS:
  
.DS_Store

### Звёздочка (*)  

 Игнорировать все файлы, которые заканчиваются на .jpeg:  
 
*.jpeg  

 Игнорировать все файлы "tmp" во всех подпапках папки docs:  

docs/*/tmp  

 Если задать правило, которое состоит только из звёздочки, Git будет игнорировать все файлы.  
 Это происходит потому, что под звёздочку подходит любое имя файла.

 Странное, но возможное правило "игнорировать все файлы":  

\* 

### Вопросительный знак (?)  
Вопросительный знак ? соответствует одному любому символу.  

file?.txt  

Если сохранить такую запись в **.gitignore**, то будут проигнорированы, например, файлы **fileA.txt и file1.txt**.  
А вот файл **file12.txt** не будет проигнорирован, потому что в его названии два символа после **file**, а не один.  

### Квадратные скобки ([…])   
Игнорировать файлы **file0.txt, file1.txt и file2.txt**  
При этом не игнорировать **file3.txt, file4.txt, ...**:  

file[0-2].txt  

В скобках можно либо перечислить символы ([abc]), либо задать диапазон ([a-z]).  

### Слеш (/)  
Косая черта, или слеш (/), указывает на каталоги.  
Если шаблон в **.gitignore** начинается со слеша, то Git проигнорирует файлы или каталоги только в корневой директории.  

Игнорировать todo.txt в корне репозитория:  

/todo.txt  

Для сравнения: spam.txt будет игнорироваться во всех папках:  

spam.txt  

Если шаблон заканчивается слешем, то правило применится только к папке.  

Игнорировать папку build:  

build/  

### Парные звёздочки (**)  
Функция парных звёздочек (\*\*) похожа на функцию одинарной (\*).  
Отличие в том, как они работают с вложенными папками.  
Двойная звёздочка может соответствовать любому количеству таких папок (в том числе нулю). Одинарная может соответствовать только одной.  

Игнорировать файлы **"docs/current/tmp", "docs/old/tmp"**,  
 а также **"docs/old/saved/a/b/c/d/tmp"**  
 и даже **"docs/tmp"**, потому что ноль вложенных папок тоже подходит:  

docs/**/tmp  

 Игнорировать только **"docs/current/tmp"** и **"docs/old/tmp"**  
 файл **"docs/old/saved/a/b/c/d/tmp"** не попадает в правило:  

docs/*/tmp  

### Восклицательный знак (!)  
Любое правило в файле **.gitignore** можно инвертировать с помощью восклицательного знака (!).  
 Игнорировать все JPEG-файлы:  

*.jpeg  

 Но только не мем с Doge:  

!doge.jpeg  

### .gitignore и git status  
Игнорируемые файлы не отображаются в выводе команды **git status**, иначе они бы засоряли вывод.  
Если всё же нужно отобразить все игнорируемые файлы, то это можно сделать с помощью ключа **--ignored: git status --ignored**.  
В таком случае в выводе **git status** появится раздел **Ignored files**.  


## 12. Клонируем репозиторий  

**git clone ссылка** - клонировать репозиторий;  
Команда **git clone** автоматически связывает локальный и удалённый репозиторий.  
То есть если в GitHub-репозитории что-то поменяется (например, добавятся коммиты), вам не нужно будет заново клонировать его.  
Достаточно будет выполнить команду, которая обновит вашу копию.  
Убедитесь в том, что репозитории связаны, командой **git remote -v**.  

## 13. Выполняем Fork  

**Fork (англ. «развилка», «ответвление»)**, или **«форк»**, — это GitHub-операция;  
Напрямую с Git она не связана. **«Форк»** создаёт копию репозитория в аккаунте GitHub.  
Такая копия будет полностью независима.  
Изменения, которые вы внесёте, не будут синхронизированы с исходным репозиторием.  
В процессе **«форка»** создаётся копия всех файлов, истории коммитов и веток.  
Эта копия сохраняется в вашей учётной записи GitHub.  
Вот некоторые из распространённых причин использования **«форков»**:  

- Вы хотите внести свой вклад в проект (например, open source), но не имеете прав на изменение исходного репозитория.  
Тогда вы можете сделать **«форк»**, добавить нужные правки, а затем отправить запрос на включение этих изменений в оригинальный проект.  
- Вы хотите развивать проект независимо от исходного.  
Допустим, создатели проекта решили, что не будут добавлять функциональность, которая вам необходима.  
В таком случае вы можете сделать «форк» и добавить её самостоятельно.  

**«Форк»** или **clone**?
 Обычно комбинация **«форк» + clone** используется для внесения изменений в публичные репозитории.  
 В этом случае «форк» становится подготовительным этапом перед клонированием чужого репозитория на ваш компьютер.  
 Если репозиторий приватный или это репозиторий вашей компании, при работе с ним достаточно **clone**.  
 Копия, которая получена с помощью **«форка»**, полностью независима от оригинального проекта — изменения не будут синхронизированы.  

## 14. Что такое ветка  

**Ветка (англ. branch)** — это изолированный поток разработки проекта. В таком потоке можно проверять разные идеи, тестировать новую функциональность и так далее.  
Благодаря веткам несколько человек могут работать над одним репозиторием и не мешать друг другу. А ещё ветки помогают декомпозировать большую и страшную задачу на маленькие и понятные.  

**git branch** - посмотреть ветки проекта;  

## 15. Создаём ветку  

**git branch <название_ветки>** - создать ветку  

В названии ветки есть слеш — что это значит?  
Название ветки в Git может состоять из букв, цифр, а также включать любой из четырёх символов: **., -, _, /**.  
Эти символы не несут особого смысла. Например, ветка **feature/add-branch-info** могла бы называться **feature_add-branch-info** или **feature-add-branch**.  
Обратите внимание, что ветки не образуют иерархии, как директории, разделённые символом **/**.  

**git branch -a** - покажи все известные ветки, как локальные так и удаленные.  

### Как назвать новую ветку  
Мы будем использовать указатели **feature** (англ. «особенность», «деталь») для веток, где прорабатывается новая функциональность, и **bugfix** (от англ. bug — «жук», «ошибка» и fix — «исправить») для веток, где ведётся работа по исправлению ошибок.  
После ключевого слова идёт слеш и описание проблемы или задачи (например, /add-branch-info). Это описание не должно содержать пробелов — следует использовать нижнее подчёркивание или дефис. В наших примерах мы будем использовать дефис.  

**git checkout <название_ветки>** - переключиться на другую ветку  
**git checkout -b <название_ветки>** - создать ветку и сразу переключиться в нее  

Ветка в Git — это указатель на коммит. Когда вы делаете новый коммит в ветке, этот указатель передвигается вперёд.  
Ветка указывает на коммит, который сделан в ней последним. При этом две ветки могут ссылаться на один и тот же коммит — например, если вы только что создали ветку, но ещё не успели внести в неё коммит.  

## 16. Сравниваем ветки  

**git diff <название_ветки1> <название_ветки2>** - сравнить ветки;  

**git diff** может сравнивать ветки по их названиям. Например, команда **git diff main feature/my-feature** выведет разницу между основной веткой и веткой **feature/my-feature**.  
Git поддерживает суффикс навигации **\~**. С его помощью можно сослаться на предыдущие коммиты.  
Например, если вы находитесь в ветке main и хотите вывести разницу между тем коммитом, который был три коммита назад, и текущим, нужно выполнить **git diff main~3 main**.  
 
## 17. Объединяем и удаляем ветки

**git merge <название_ветки>** - выполнить слияние;  

Перед тем как начать процесс слияния, нужно перейти в ветку, куда должны добавиться изменения. Обычно это главная ветка.  
Перейдите в неё и вызовите команду **git merge** с именем присоединяемой ветки **feature/diff** в качестве параметра.  

**git branch -D <название_ветки>** - удалить ветку после слияния.  
**git branch -d br-name** - удалить ветку, но только если она является частью main  

После того как произошло слияние, ветку-донора можно удалить. Для этого в основной ветке введите команду **git branch с флагом -D** (от англ. delete — «удалить») и названием ветки.  
Если в момент удаления вы будете находиться в той ветке, которую хотите удалить, Git сообщит об **ошибке: can not delete branch** (англ. «не получается удалить ветку»).  
У команды **git branch -D** есть более безопасный вариант с **флагом -d**.  
Он удалит ветку только если она была полностью объединена с другой — то есть если две ветки стали (или изначально были) частью одной истории.  
Например, если вы нечаянно создали ветку с неправильным названием, её можно удалить через **git branch -d %имя_ветки%**.  
 
_Удаление локальной ветки через Git не удаляет ветку на GitHub!_  

## 18. Создаём pull request  

**Пул-реквес** — это запрос на рассмотрение предлагаемых изменений и часть процесса ревью.  
Нельзя просто внести правки в своей ветке и сразу залить её в основную. Сначала ваши коллеги должны убедиться, что предложенные вами изменения логичны и эффективны.  
Для этого используют механизм **pull request**.  

Алгоритм такой:

1. Вы трудитесь над задачей в своей ветке — например, пишете код новой функциональности.  
2. Вы заканчиваете работу, а затем создаёте пул-реквест.  
3. Ваши коллеги проверяют, что код выглядит аккуратно и лаконично, а программа работает корректно; также оставляют комментарии.  
Этот процесс называют **code review** (англ. «рассмотрение кода»), или просто ревью.  
4. После финального согласования вы заливаете свою ветку в основную.  

### Из чего состоит **pull request** и чем он может обернуться  

У каждого пул-реквеста есть:  

1. Название — краткое описание предлагаемых изменений. Например: **Адаптивный заголовок сайта, Замена альбома на галерею** и так далее.  
2. Описание — развёрнутое описание изменений. Это поле заполнять необязательно, но желательно.  
3. Исходная ветка — та, в которой вы работали. Например, **feature/merge-request**.  
4. Целевая ветка — основная ветка проекта, в которую вы хотите внести изменения.  

Также у каждого пул-реквеста может быть два исхода:  

**merge** (англ. «соединить») — предлагаемые изменения приняты; код вливается в целевую ветку; пул-реквест закрывается.  
**close** (англ. «закрыть») — пул-реквест закрывается без слияния изменений.  

Запрос на изменения можно инициировать двумя способами: **через ссылку**, которую Git выводит после создания ветки, или **через интерфейс GitHub**.  
После создания **пул-реквеста** ваши коллеги сделают **ревью** — оценят предложенные вами правки и оставят свои комментарии.  
По результатам **ревью** ваши правки могут быть приняты в основную ветку проекта или возвращены на доработку.  

## 19. Забираем изменения из удалённого репозитория  

**git pull** - забрать изменения из удаленого репозитория.  

Обычно **git pull** — это первая команда, которую вводит разработчик, как только открывает код проекта, чтобы начать с ним работать.  
Дополнительно **git pull** и **git merge** выполняют перед тем, как создать пул-реквест.  
При командной работе, особенно в больших командах, основная ветка часто успевает **«убежать» вперёд**, пока вы подготавливаете свои изменения.  
Поэтому перед созданием пул-реквеста рекомендуется сначала подтянуть изменения из основной ветки, объединить их с вашей, решить все возможные конфликты и лишь затем сделать **push**.  

_Перед созданием нового пул-реквеста считается хорошей практикой перейти в главную ветку, «подтянуть» в неё изменения, а затем добавить эти изменения в вашу ветку с помощью **git merge main**._  

**git remote rm origin** - удалить текущий привязанный origin (при форк проекта).  

Удадить коммиты с ГитХаб:

**git reset --hard <хэш>**  
**git push --force**   

## 20. Что такое fast-forward  

- При слиянии этих двух веток никак не возможен конфликт;  
- Истории этих двух веток не «разошлись»;  
- Одна ветка является продолжением другой. 
 
Обратите внимание на два момента:  

- При слиянии веток Git выводит строку **Fast-forward**.  
- В истории коммитов **HEAD** указывает одновременно и на **main**, и на **add-docs**. После такого слияния эти ветки одинаковые: в них одни и те же коммиты.  

### Можно отключить fast-forward  

**Fast-forward** слияние веток можно отключить флагом **--no-ff**.  

Например: **git merge --no-ff add-docs**.  

Также его можно **отключить «навсегда»** (до тех пор, пока вы не вернёте настройку «как было») с помощью настройки **merge.ff: git config [--global] merge.ff false**.  

Если отключить слияние в режиме **fast-forward**, вместо «перемотки» ветки Git создаст в ней коммит слияния (англ. merge commit) — в обиходе его называют merge-коммит или мёрж-коммит:  

**$git log --graph --oneline**
  
*   6814789 (HEAD -> main) Merge branch 'add-docs'  
|\  
| * e08fa2a (add-docs) New docs 2  
| * fd588b2 New docs 1  
|/  
* 997d9ce Commit 4  
* 0313e8e Commit 3  
* 5848aba Commit 2  
* 04923d7 Commit 1   

Многие проекты отключают **fast-forward** слияние веток, потому что при нём теряется часть информации.  
Результат выглядит так, как будто в main «просто появились» новые коммиты.  
Если не знать о ветке add-docs, то можно подумать, что такой ветки и не было.  
Полноценный коммит слияния сохраняет всю информацию: в нём будет указано, какая именно ветка вливалась в main.  

## 21. Non-fast-forward  

Вернёмся к примеру с ветками main и add-docs и представим такую ситуацию: истории двух веток **«разошлись»**.  
Это значит, что их коммиты уже нельзя выстроить в одну линию.  
Например, после «отделения» add-docs в ветку main добавили новый коммит Commit 5.  

Команде git log можно указать несколько веток, и тогда она выведет их все:  

**$ git log --graph --oneline main add-docs**
  
* 15d3f04 (HEAD -> main) Commit 5  
| * 8de42eb (add-docs) New docs 2  
| * 4d3c346 New docs 1  
|/  
* 73def1e Commit 4  
* 9c30ab3 Commit 3  
* 83cc5ec Commit 2  
* 8e87fb2 Commit 1  

Когда Git проверяет ветки на состояние **fast-forward**, он не «заглядывает» в файлы и не пытается угадать, будет ли конфликт на самом деле.  
Для Git важно только, что конфликт теоретически возможен (или, наоборот, никак не возможен)  

Находимся в ветке main, **--no-edit** избавляет от необходимости вводить сообщение для merge-коммита:  

**$ git merge --no-edit add-docs**  

Merge made by the 'ort' strategy.  
 docs.txt | 1 +  
 1 file changed, 1 insertion(+)  
 create mode 100644 docs.txt  

 коммит слияния: 34f5f8f  

**$ git log --graph --oneline**  

*   34f5f8f (HEAD -> main) Merge branch 'add-docs'  
|\  
| * 8de42eb (add-docs) New docs 2  
| * 4d3c346 New docs 1  
* | 15d3f04 Commit 5  
|/  
* 73def1e Commit 4  
* 9c30ab3 Commit 3  
* 83cc5ec Commit 2  
* 8e87fb2 Commit 1   

Если конфликтов при слиянии нет, команда git merge отработает почти автоматически — только предложит вам ввести сообщение для нового коммита слияния.  
Чаще всего сообщения к коммитам слияния не редактируют и оставляют «как предложил Git».  
Для таких случаев удобен флаг **--no-edit: git merge --no-edit %another_branch%**.  
Если конфликты всё-таки есть, Git сначала попытается разрешить их автоматически. Если не получится, Git предложит вам разрешить их вручную.  

## 22. git push и fast-forward  

Ветка **main** находится на локальном компьютере, а **main@origin** — в репозитории на GitHub.  
Если **main** и **main@origin** находятся между собой в состоянии **fast-forward** (main@origin можно просто «перемотать» до того же состояния, что и main), то git push так и сделает.  
В итоге локальная и удалённая ветки будут содержать одинаковый набор коммитов.  

### git push и не-fast-forward  

Представим, что ветки **main** и **main@origin** находятся в таком состоянии: в ветке **main@origin** есть коммиты C1C1​, C2C2​ и DD, а в **main** — C1C1​, C2C2​, C3C3​, C4C4​.  
Ветки **main** и **main@origin** «разошлись», то есть находятся в состоянии **не-fast-forward**. Если теперь попытаться выполнить команду **git push**, она выведет следующую ошибку:  

текущая ветка — **main**
  
**$ git push**
  
To github.com:username/repository.git  
 ! [rejected]        main -> main (non-fast-forward)  
error: failed to push some refs to 'github.com:username/repository.git'  
hint: Updates were rejected because the tip of your current branch is behind  
hint: its remote counterpart. Integrate the remote changes (e.g.  
hint: 'git pull ...') before pushing again.  
hint: See the 'Note about fast-forwards' in 'git push --help' for details.  

_Обратите внимание на надписи **rejected** (англ. «запрос отклонён») и **non-fast-forward** — Git подсказывает, что именно пошло не так._  

### Пара слов о rebase  

В Git можно решить проблему «разошедшихся» веток с помощью операции rebase (англ. «перебазирование»).  
Эта операция позволяет изменить точку (коммит), от которой отделилась ветка.  
После такого перебазирования ветки будут в состоянии **fast-forward**, и **git push** сработает без ошибок.  

Однако у такого шага могут быть последствия. Например:  

- Могут возникать конфликты между изменениями, как при слиянии веток;  
- Если действовать неаккуратно, можно «сломать» репозиторий.  

### Пара слов о **git push --force**  

Есть и другой способ справиться с ошибкой **rejected: non-fast-forward** — это форсированный пуш.  
Чтобы его выполнить, используют **флаг --force** (англ. «сила», «заставить»).  
В очень редких случаях это уместная команда.  
Например, если кто-то нечаянно «сломал» ветку **main@origin**, можно найти копию репозитория, в которой ветка main не «сломана», и использовать **git push --force** для восстановления ветки в **origin**.  

## 23. Почему бы не «пушить» всё в main  

Команда **git push** ожидает, что локальная ветка и её удалённая версия не **«разошлись»**, то есть одна может просто **«догнать»** другую без конфликтов.  
Если несколько человек будут **«пушить»** коммиты прямо в **main**, локальная ветка **main** и ветка **main на GitHub** будут постоянно **«расходиться»** у других участников команды.  

## 24. Модели веток. Простая feature branch модель  

**Подходы к работе с ветками** — это правила, которые описывают, когда и для чего создаются ветки, какие в них коммиты и в какой момент происходит слияние веток.  

**Feature branch workflow** — простой и самый популярный вариант. Если коротко, в нём для каждого нового изменения создаётся новая ветка, которая позже вливается в **main** с помощью **git merge**.  
Если аккуратно следовать подходу **feature branch workflow**, то:

- Не будет проблемы «расхождения» веток, ведь новые изменения попадают в **main** через **git merge**, а не через **git push**.  
Команду **merge** «разошедшиеся» ветки не смущают, ведь для них она и придумана.  
- В ветке **main** всегда рабочая версия проекта.  
Все «полуфабрикаты» и недоделанные функциональности находятся в **feature-ветках**, пока не будут готовы попасть в **main**.  

**Git flow** — более сложный вариант. Подход похож на **feature branch workflow**, но в нём создаётся больше веток, а изменения (коммиты) делят на разные типы: исправление, новая функциональность и так далее.   
Разные типы коммитов попадают в разные ветки.  

**Trunk-based** — популярный в больших компаниях (таких как Яндекс, Google и прочих) подход, который обещает бо́льшую скорость работы в крупных командах.  
Этот подход тоже похож на **feature branch workflow**. Главное отличие в том, что участники проекта вливают (merge) свой код в основную ветку максимально часто. Например, каждый день.  

- Разные компании и команды используют разные модели работы с Git. Эти модели описывают структуру веток в проекте, а также правила создания и слияния коммитов в них.  
- Один из самых простых и популярных подходов — **feature branch workflow**. Он предполагает, что работа над функциональностью ведётся в отдельной **feature-ветке**. Когда всё готово, эта ветка вливается в основную.  
- Подход **feature branch workflow** — лишь шаблон, по которому можно действовать. Многие компании и команды меняют его под свои нужды, но неизменно одно: хочешь сделать новую функциональность или исправить баг — создай новую ветку!  

## 25. Pull request и code review  

В большинстве команд новые функциональности и исправления попадают в **main** через запрос на слияние (англ. **pull request, или merge request**).  
Его так и называют — пул-реквест или мёрж-реквест. В переводе с языка Git это значит: «Вот моя ветка, хочу «вмёржить» её в main».  

Названия «пул-реквест» и «мёрж-реквест» означают одно и то же. GitHub и BitBucket используют термин «пул-реквест», а GitLab — «мёрж-реквест».  

**«Запросы на слияние»** — это та часть процесса (workflow), которая может сильно отличаться от команды к команде.  
Например, в некоторых проектах строго следят за качеством изменений и тщательно проверяют их до того, как влить в main. А некоторые проще относятся к тому, что попадает в основную ветку.  
На этапе пул-реквеста можно сделать разные проверки. 
Например:  

- Запустить автоматические тесты, которые покажут, не «сломают» ли новые изменения уже существующую в проекте логику;  
- Просмотреть изменения «глазами» — это называется **code review** (англ. «осмотр», «рецензия кода») или просто **review**. Мы будем использовать вариант написания «ревью».  
 
Во многих командах пул-реквест — это основной путь, по которому изменения или исправления попадают в основную ветку проекта.  
Важный этап пул-реквеста — ревью. В ходе ревью коллега оценит правки и предложит доработки, если они нужны.  
Когда всё будет готово, ревьюер примет («апрувнет») изменения, затем их можно будет интегрировать в main.  

В реальных проектах перед «отделением» **feature-ветки** стоит обновлять локальную ветку **main** (**git checkout main && git pull**), чтобы ваша ветка «росла» от последнего коммита основной.  
Так вы уменьшите вероятность конфликтов слияния в будущем, когда будете вливать вашу ветку обратно в main.  

GitHub вливает ваши изменения в ветку **main в origin**, а локальная ветка остаётся как была. После «мёржа» PR рекомендуем обновить локальную **main: git checkout main && git pull**  

## 26. Разрешение конфликта вручную и через vimdiff  

### Разрешаем конфликт вручную  

Если выполнить **git status** в процессе «мёржа», файлы с маркерами конфликтов будут отображаться в особой категории **Unmerged paths** (англ. «не соединённые пути») с текстом both modified (англ. «оба изменены»).  
Вывод будет такой:  

**$ git status**  

On branch main  
You have unmerged paths.  
  (fix conflicts and run "git commit")  
  (use "git merge --abort" to abort the merge)  

Unmerged paths:  
  (use "git add <file>..." to mark resolution)  
    both modified:   readme.md   

При попытке объединить ветки или применить изменения из удалённого репозитория Git добавит в файлы специальные маркеры конфликта.  
Убедитесь в этом. Откройте файл readme.md в графическом интерфейсе или выполните cat readme.md. Вы увидите следующее.  

**$ cat readme.md**    

    ````<<<<<<< HEAD  
	version 1  
	=======  
	version 2  
	>>>>>>> br2   

Git разметил файл. Получившиеся секции содержат изменения из каждой ветки:  

    Текст между <<<<<<< HEAD и ======= указывает на изменения, которые находятся в HEAD — в данном случае это ветка main. Здесь окажутся только те строки, в которых есть конфликт.  
    Текст между ======= и >>>>>>> br2 показывает на изменения, которые находятся в ветке br2.  

Чтобы разрешить конфликт вручную, нужно открыть файл и выбрать, какие изменения оставить, а какие отбросить.  
Для этого следует удалить все маркеры и ненужные изменения и оставить нужные.  
После разрешения конфликта файлы будут отмечены как решённые.  
Можно продолжить процесс слияния или выполнить коммит изменений.  
Допустим, нужно оставить текст **version 2**. Откройте файл readme.md и удалите все маркеры конфликтов, а также строку **version 1**.  
Должно получиться следующее.  

version 2  

Подготовьте изменения к сохранению и сделайте коммит.  

**$ git add . && git commit --no-edit**  

### Разрешаем конфликт через инструмент слияния vimdiff  

В ходе курса вы наверняка не раз сталкивались с редактором **Vim** в консоли.   
Он также предоставляет инструмент слияния, который называется **vimdiff**.   
Чтобы его вызвать, при возникновении конфликта нужно выполнить команду **git mergetool**.  

Имитируем конфликт из урока и вызываем vimdiff командой **git mergetool**.  
После сообщения в консоли **Hit return to start merge resolution tool (vimdiff)** (англ. «нажмите „вернуть“, чтобы запустить инструмент разрешения конфликтов»), нажимаем Enter, чтобы открыть vimdiff.  
vimdiff показывает четыре окна:  
 
- в верхнем левом углу — текущая версия файла в HEAD;  
- в правом верхнем углу — версия из ветки br2;  
- посередине сверху — версия из ветки, которая является общим предком, то есть из main;  
- снизу — результат изменения с маркерами конфликта.  

**vimdiff** создаёт копию конфликтного файла с маркерами изменений и расширением .orig. Этот файл можно удалить после слияния.  
После успешного слияния выполняем коммит. Он станет коммитом слияния.  

Команды **git gl** не существует в Git. Это сокращённая запись, которую можно создать для любой команды через механизм alias (англ. «псевдоним»).  
Подробнее о нём можно почитать в документации.
 
 Вызов **git gl** превращается в вызов **git log** с несколькими параметрами: **git log --oneline --abbrev-commit --graph --date=short --pretty=format:'%h - %an, %cd : %s**'.  
У каждого флага своя функция. **--abbrev-commit** покажет только первые несколько символов из хеша коммита; **--graph** выведет результат в виде графа; **--date=short** выведет дату в формате yyyy-MM-dd, например 2023-07-12; **--pretty=format:'%h - %an, %cd : %s'** задаёт формат выдачи результата.  

## 27. Разрешение конфликта через Visual Studio Code  

У **VS Code** есть более мощный графический интерфейс для конфликтов.  
Чтобы его открыть, нажмите на кнопку **Resolve in Merge Editor**.  
Вы увидите окно разрешения конфликтов.  
Оно состоит из трёх частей: в левой части содержатся новые изменения, в правой — текущие, а в нижней — результат.  
Разрешите конфликт с помощью VS Code и выполните коммит слияния.  

## 28. Что делать, если основная ветка «убежала» вперёд в процессе ревью  

**Конфликт** — это не ошибка, а особенность командной работы.  

Представьте: вы создаёте пул-реквест, чтобы добавить свои изменения из ветки **feature/my-new-awesome-code** в основную ветку **main**.  
В это время в **main** вливается ветка другого коллеги (**feature/other-colleague-code**), которая попала на ревью раньше вашей, и передвигает **main** вперёд.  
Теперь на GitHub новая версия репозитория.  
А локально у вас всё ещё старая.  
Теперь ваши изменения отстают от ветки **main**. Дальше может быть два варианта развития событий.  

Первый: ваши изменения и текущие изменения в **main** получится **«смёржить» автоматически**, потому что GitHub сможет самостоятельно разрешить конфликт.  
Второй: два изменения не могут существовать вместе, и вы увидите предупреждение.  

Разрешить конфликт можно так:  

1. Перейти в ветку **main**.  
2. Загрузить новые изменения из неё с помощью **git pull**. При этом вы также загрузите ветку вашего коллеги.  
3. Снова перейти в вашу ветку **feature/my-new-awesome-code**.  
4. Выполнить **git merge main** и разрешить конфликт локально. В результате будет создан локальный коммит слияния.  
5. Отправить изменения из вашей ветки в репозиторий с помощью **git push**. Так коммит слияния попадёт в удалённый репозиторий и в пул-реквест.  
Теперь, когда ваши изменения пройдут ревью и окажутся в **main**.  


# Алгоритм-шпаргалка для создания PR  

    1. Склонировать репозиторий.  
       1.1. Если вы не участник проекта, предварительно сделать «форк» исходного репозитория.  
       1.2. На странице репозитория или «форка» нажать кнопки: Code → SSH → скопировать ссылку.  
       1.3. Выполнить команду git clone <ссылка на репозиторий>.  
    2. Создать ветку для вашей задачи: git checkout -b my-task-branch-name.  
    3. Добавить и «закоммитить» изменения, которые вы хотите внести в проект.  
    4. «Запушить» ветку: git push --set-upstream origin HEAD или git push -u origin my-task-branch-name.  
        4.1. GitHub (с помощью Git) выведет ссылку на создание PR. По ней нужно перейти.  
        4.2. PR можно также создать через интерфейс GitHub.  
    5. Сообщить о пул-реквесте ревьюеру.  
        5.1. Иногда ревьюеры назначаются автоматически, тогда сообщать не нужно.  
    6. Обсуждать с ревьюером предлагаемые изменения и вносить правки, пока эти изменения не будут одобрены (пока не будет получен «апрув»).  
        6.1. Если кто-то добавил конфликтующие изменения в main, пока ваш PR был на ревью, нужно разрешить конфликт:  
        - Обновить main: git checkout main && git pull.  
        - Влить main в свою ветку: git checkout my-task-branch-name && git merge main.  
        - Разрешить конфликты слияния с помощью IDE или вручную.  
        - Создать коммит слияния: git commit --no-edit или git commit -m 'merge main'.  
        - Сделать git push своей ветки.  
    7. Нажать кнопку Merge или подождать, пока её нажмёт кто-то ещё.  
    8. Ещё раз обновить main, чтобы «подтянуть» ваши изменения в основную ветку локального репозитория: git checkout main && git pull.  
    9. Вы великолепны! Можете начинать снова со второго пункта.

# Алгоритм-шпаргалка для разрешения конфликтов слияния  

    1. Открыть проект в IDE (VS Code, IDEA или другие).  
    2. Открыть файл, в котором есть конфликт.  
    3. Выбрать, какие части файла нужно взять из одной ветки, а какие — из другой.  
    4. Когда конфликты разрешены, сделать коммит: git commit --no-edit или git commit -m 'merge branch <название ветки>'.  