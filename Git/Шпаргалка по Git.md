# Шпаргалка по Git
Источники:
- [Learn Git Branching](https://learngitbranching.js.org/)
- [Git Commit | SKILLFACTORY MEDIA](https://blog.skillfactory.ru/glossary/git-commit/)
- [Git: Очередной лист Вопросов и Ответов | Хабр](https://habr.com/ru/articles/813513/)

### Создание коммита
```bash
git commit -m "message"
```

### Создание новой ветки
```bash
git branch <name>
```

### Выбор существующей ветки
```bash
git checkout <name>
```

### Создание и одновременный выбор ветки
```bash
git checkout -b <name>
```

Можно вытворять такое:
```bash
git checkout -b <name> <commit-hash>
```

### Слияние с мёрдж-коммитом (git merge)
Находясь в **main**, мёрдж ветки **feature**:
```bash
git merge feature
```

### Слияние без мёрдж-коммита (git rebase)
Находясь в **feature**, ребэйс на **main**:
```bash
git rebase main
```

Может принимать \<dst> и \<src> (как бы в таком порядке...).

Если ветка **main** была предком **feature**, то _git rebase feature_ (находясь в main) просто передвинет **main** на коммиn **feature**.

### HEAD detaching
Присвоение HEAD не ветке, а конкретному коммиту:
```bash
git checkout <commit-hash>
```

C помощью относительных ссылок:
```bash
git checkout <branch-name>~N
```

При N == 1 можно воспользоваться ^:
```bash
git checkout <branch-name>^
```

Можно также использовать сам HEAD:
```bash
git checkout HEAD^
```

### Перемещение ветки (branch forcing)
```bash
git branch -f <src> <dst>
```

### Отмена изменений
_git reset_ подоходит для локальных изменений. _git reset_ перенесёт ветку назад, как будто некоторых коммитов вовсе и не было:
```bash
git reset HEAD~1
```

_git revert_ -- для удалённых веток. Создаётся коммит с изменениями, противоположными отменяемому (можно использовать HEAD):
```bash
git revert <commit-name>
```

### cherry-pick
Копирование отдельных коммитов туда, где в данный момент HEAD:
```bash
git cherry-pick <commit-hash-1> <commit-hash-2> <...>
```

### Интерактивный rebase:
```bash
git rebase -i <src>
```

Позволяет выбрать нужные коммиты, объединить их, выкинуть или поменять порядок.

### git commit --amend
Если нужно изменить последний коммит, но вы не внесли новые изменения, введите команду git commit -amend в терминале. Она открывает текстовый редактор по умолчанию, где можно отредактировать сообщение коммита. После внесения изменений просто сохраните файл. Если вам нужно добавить новые правки к последнему коммиту, сначала внесите их в свои файлы, затем выполните команду git add, чтобы указать их в индексе. Затем запустите команду git commit -amend, которая объединит новые правки с предыдущим коммитом. 

### Создание локальной копии удалённого репозитория
```bash
git clone
```

### git fetch
Cинхронизирует локальное представление удалённых репозиториев с тем, что является актуальным на текущий момент времени.

Важно отметить, что команда git fetch забирает данные в ваш локальный репозиторий, но не сливает их с какими-либо вашими наработками и не модифицирует то, над чем вы работаете в данный момент.

### git pull
git pull == git fetch && git merge origin/main

Также можно:
```bash
git pull --rebase
```

### git push
Команда git push отвечает за загрузку ваших изменений в указанный удалённый репозиторий, а также включение ваших коммитов в состав удалённого репозитория.

### Работа с изменившемся удалённым репозиторием:
```bash
git pull (--rebase)
git push
```

### git stash
Команда которая сохраняет текущие не закомиченные изменения в локальном хранилище.
```bash
# Показывает список всех stash записей
git stash list

# Сохранить изменения в stash
git stash
git stash save [name_in_stash_list]

# Выгружает изменения из stash в текущую ветку
# для работы, удаляя запись
git stash pop

# Выгружает изменения из stash в текущую ветку
# для работы, но не удаляет запись
git stash apply [--index [index]]

# Удаляет запись из stash 
git stash drop
# Удаляет все наборы отложенных изменений
git stash clear
```


## git config
```bash
git config --global user.name "username"
git config --global user.email "mail@mail.com"
git config --list
git config --global credential.helper store
```
