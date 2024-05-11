**Поэтапная работа с Git/GitHub**

1. Установить Git на компьютер (<https://git-scm.com./download/win>)
2. Настройка Git (указать автора)

   git config   - -global user.name “<ВАШЕ ИМЯ>”

   git config   - -global user.email “<АДРЕС ПОЧТЫ>”

3. Создание репозитория

   нужно перейти в папку проекта (которую нужно отслеживать)

   cd <путь к папке проекта>

   git init

4. Создание commit

   git add .  (добавить все файлы проекта в будущий commit)

   git add   - -all (добавить все файлы проекта в будущий commit)

   git add <ИМЯ ФАЙЛА> (конкретный файл)

   git commit  -m “<комментарий”>

5. Просмотр commit (изменения статуса commit)

   git status

 - untracked (не отслеживаемый) – в рабочей директории, но нет ни в одной версии HEAD / Git не знает о файле)

 - modified (изменен) – в рабочей директории есть более новая версия по сравнению с HEAD / изменения не находятся в следующем commit

 - staged (подготовлен) - готов к commit
 
    ```mermaid
    graph LR;
       A(untracked) -- "git add" --> B(staged);
       C(staged) -- "git commit -m" --> D(tracked/comitted);
    ```

6.  Просмотр изменений

   git log

7. Удаленный репозиторий

   а) необходимо создать новый репозиторий в GitHub

        - даем имя (как имя папки)

        - выбираем public / private

        - создаем

   б) связываем удаленный репозиторий на GitHub с локальным, на компьютере Git

        - генерируем SSH-ключ (сетевой протокол Secure Shell Protocol)

            Приватный ключ (Только для вас. Хранится на вашем компьютере. Используется для расшифровки данных)

            Публичный ключ (Доступен всем и используется для расшифровки данных)

                ls  -la .ssh/ (проверяет наличие ключей)

                ls  -a ~/.ssh (проверяет наличие ключей)

        - привязываем SSH-ключ к GitHub

        - связываем удаленный и локальный репозиторий

            git remote add origin git@github.com:%ИМЯ АККАУНТА%/ИМЯ ПРОЕКТА.git

            origin – имя удаленного репозитория (по умолчанию)

            ИМЯ АККАУНТА (URL) – копируем со страницы удаленного репозитория

        - убедиться, что репозитории связаны

            git remote  -v
			
8. Отправить закоммиченный файл на удаленный репозиторий
    
	git push /если надо после указать кодовое слово/
	
9. Добавить файл в последний коммит (--amend от англ.amend - "исправить", "дополнить")

    mkdir <название папки> - создали папку
	
	cd <название папки> - перешли в созданную папку
	
	touch <название файла.расширение файла> - создали файл (например создали файлы: main.html и common.css)
	
	git init - создали репозиторий (папка теперь отслеживается на ПК, локальный репозиторий)
	
	git add <название файла> - добавили файл в будущий коммит (например: main.html)
	
	git commit -m "текст коммита"  - закоммители файл (main.html, с коммитом "Добавить главную страницу")
	
	git add <название файла> - добавили файл в будущий коммит (например: common.css)
	
	git commit --amend --no-edit  - добавили файл common.css в коммит "Добавить главную страницу", без изменения коммита
	
        --amend   -  опция добавляет файл в последний коммит
	
	    --no-edit   -опция сообщает команде commit, что сообщение коммита нужно оставить как было
		
	ВАЖНО!!! команда git commit --amend работает только с последним коммитом(HEAD). Для исправления других коммитов существуют другие комманды.
	
10. Изменить сообщение коммита

      Пример: заменим коммит "Добавить главную страницу" на "Добавить главную страницу и стили" без добавления файла в коммит
      
      git commit --amend -m "Добавить главную страницу и стили"
      
	  git log --oneline
	  
	  d7d6g34 Добавить главную страницу и стили
	  
	  (Хеш коммита снова поменялся, потому что изменились сообщение и время коммита. Файлы в комите осталить теме же)
	  
11. Как откатиться назад, если всё сломалось:
	  
	a) Выполнить unstage изменений - git restore --staged <имя файла>
	
		    Пример:
		
		    $ touch example.txt # создали ненужный файл
		
		    $ git add example.txt # добавили его в staged

		    $ git status # проверили статус
		
		    Changes to be committed:
		
			    (use "git restore --staged <file>..." to unstage)
			
			    new file:   example.txt

		    $ git restore --staged example.txt
		
		    $ git status # проверили статус

		    Untracked files:
		
			    (use "git add <file>..." to include in what will be committed)
			
				    example.txt

		    no changes added to commit (use "git add" and/or "git commit -a")
		
		    # файл example.txt из staged вернулся обратно в untracked 
		
		Вызов git restore --staged example.txt перевёл example.txt из staged обратно в untracked.
		
		Чтобы «сбросить» все файлы из staged обратно в untracked/modified, 
		
		можно воспользоваться командой git restore --staged .: 
		
		она сбросит всю текущую папку (.).
		
	б) «Откатить» коммит — git reset --hard <commit hash>
	
			Иногда нужно «откатить» то, что уже было закоммичено, 
			
			то есть вернуть состояние репозитория к более раннему. 
			
			Для этого используют команду git reset --hard <commit hash> 
			
			(от англ. reset  — «сброс», «обнуление» и hard — «суровый»).
			
			Пример:
			
			$ git log --oneline # хеш можно найти в истории
			
			    7b972f5 (HEAD -> master) style: добавить комментарии, расставить отступы
			
			    b576d89 feat: добавить массив Expenses и цикл для добавления трат # вот сюда и вернёмся
			
			    4b58962 refactor: разделить analyzeExpenses() на countSum() и saveExpenses()
						
			$ git reset --hard b576d89
			
			# теперь мы на этом коммите
			
			HEAD is now at b576d89 feat: добавить массив Expenses и цикл для добавления трат

			Будьте осторожны с командой git reset --hard! 
			
			При удалении коммитов можно потерять что-то нужное.
			
	в) «Откатить» изменения, которые не попали ни в staging, ни в коммит, — git restore <file>
	
			Может быть так, что вы случайно изменили файл, который не планировали. 
			
			Теперь он отображается в Changes not staged for commit (modified). 
			
			Чтобы вернуть всё «как было», можно выполнить команду git restore <file>.
			
			Пример:
			
			# случайно изменили файл example.txt
			
			$ git status
			
			  On branch main
			
			  Changes not staged for commit:
			
			    (use "git add <file>..." to update what will be committed)
			
			    (use "git restore <file>..." to discard changes in working directory)
					
					modified:   example.txt
			
			$ git restore example.txt
			
			$ git status
			
			  On branch main
			
			  nothing to commit, working tree clean 
			  
			Изменения в файле «откатятся» до последней версии, 
			
			которая была сохранена через git commit или git add.
			
12. Просматриваем изменения в файлах

	  - Команда git diff используется для просмотра изменений в файлах после коммита.
	  
		Она сравнивает последнюю версию файла с текущей (изменённой) версией.
		
	  - Вывод git diff содержит информацию о том, какие строки были удалены, добавлены или сохранены.
		
		Пример:
		
		$ mkdir ~/dev/teremok //создали папку teremok
		
		$ cd ~/dev/teremok //перешли в папку teremok
		
		$ git init //создали репозиторий папки teremok
		
		$ touch teremok.txt //создали файл teremok.txt
		
		//отредактируйте файл teremok.txt, добавьте в него строки:
		
		//Теремок стоит, и в нём: никого нет
		
		$ cat teremok.txt //просмотрели содержимое файла teremok.txt
		
		Теремок стоит, и в нём: никого нет
		
		$ git add teremok.txt //добавили файл teremok.txt в список будущего коммита

		$ git commit -m "Исходное состояние теремка" //создали коммит
		
		//Откройте и отредактируйте файл teremok.txt, чтобы вместо никого нет стало Мышка-норушка. 
		
		//Сохраните файл, но не делайте коммит. 
		
		//Затем воспользуйтесь командой git status, чтобы посмотреть, что происходит с файлами.
		
		$ git status //просмотрели статус файла teremok.txt
		
		$ git diff //сравнили последнюю версию файла a/teremok.txt c текущей b/teremok
		
			___________________________________________________________________________
		
			$ git diff
			
			diff --git a/teremok.txt b/teremok.txt
			
			index f62ab9d..ef6214d 100644
			
			--- a/teremok.txt
			
			+++ b/teremok.txt
			
			@@ -1 +1 @@
			
			-Теремок стоит, и в нём: никого нет
			
			\ No newline at end of file
			
			+Теремок стоит, и в нём: Мышка-норушка
			
			\ No newline at end of file
			
			___________________________________________________________________________
			
			Самое важное git diff выводит в конце:
			
			красный цвет строки никого нет значит, что эта строка была удалена;
			
			зелёный цвет строки Мышка-норушка значит, что она была добавлена.
			
			Не все консоли умеют выводить цвета, поэтому строки помечаются не только цветом, но и знаком - или +. 
			
			Минус — это удалённые строки, плюс — это добавленные.
			
			Коротко разберём остальные строки вывода команды:
			
			Первые две строки (diff --git a/... b/... и index f62ab9d..ef6214d 100644) — это низкоуровневая техническая информация. 
			
			Мы не будем на ней останавливаться.
			
			Строки --- a/teremok.txt и +++ b/teremok.txt говорят, что дальше будет выведен результат сравнения файлов 
			
			a/teremok.txt и b/teremok.txt — исходной и текущей версий.
			
			Строка @@ -1 +1 @@ сообщает, какие строки файла попали в сравнение. 
			
			Выражение 1 (неважно, с плюсом или с минусом) говорит, что были использованы одна строки, начиная с первой. 
			
			Если бы было, например, написано +15,7, это значило бы, что в сравнении участвуют 
			
			7
			
			7 строк, начиная с 
			
			15
			
			15-й.
			
			Выражение со знаком минус (-1) относится к «оригинальной» версии файла (a/teremok.txt), 
			
			а со знаком плюс (+1) — к «изменённой» (b/teremok.txt).

	  - Флаг --staged позволяет просматривать изменения в staged-файлах.
	  
		$ git add teremok.txt //добавили файл teremok.txt в список коммита
		
		$ git diff //проверили изменения в файле
		
		//команда не выведет ничего!  //так как по умолчанию git diff не показывает изменения в staged-файлах — только в modified.
		
		//Чтобы всё-таки просмотреть изменения в staged, нужно использовать флаг --staged: git diff --staged.
		
		$ git diff --staged //посмотрели изменения в файле teremok.txt, подготовленный к коммиту
		
		___________________________________________________________________________
		
		diff --git a/teremok.txt b/teremok.txt
		
		index f62ab9d..ef6214d 100644
		
		--- a/teremok.txt
		
		+++ b/teremok.txt
		
		@@ -1 +1 @@
		
		-Теремок стоит, и в нём: никого нет
		
		\ No newline at end of file
		
		+Теремок стоит, и в нём: Мышка-норушка
		
		\ No newline at end of file
		
		___________________________________________________________________________
		
			  
	  - Git diff и git diff --staged полезны для просмотра изменений в файлах.
	  
13. Сопоставляем коммиты

	  Если вдруг на каком-то этапе работы возникнет проблема, 
	  
	  это поможет разобраться, что конкретно изменилось в одном коммите по сравнению с другим.
	  
	  Чтобы продолжить сказку, вам нужно будет дописывать новые строки в конец файла teremok.txt. 
	  
	  Для этого подходит команда echo (англ. «эхо»).
	  
	  Сама по себе эта команда просто выводит в консоль то, 
	  
	  что ей передали в качестве параметра.
	  
			$ echo "Привет!"
			
			Привет! 
			
	  Но если скомбинировать echo с символами перенаправления вывода >> (два знака «больше»), 
	  
	  то всё, что должно было попасть на экран, вместо этого будет записано в файл.
	  
			$ cat file.txt
			
			Первая строка файла

			
			$ echo "Вторая строка файла" >> file.txt
			
			$ cat file.txt
			
			Первая строка файла
			
			Вторая строка файла 
			
	  Оператор >> — это возможность командной строки (Bash). 
	  
	  Его можно использовать не только с echo, но и с любой другой командой, 
	  
	  которая выводит что-то на экран.
	  
	  Одинарный символ > тоже перенаправит вывод команды в файл, 
	  
	  но перед этим сотрёт содержимое файла, то есть перезапишет файл целиком.
	  
			$ cat file.txt
			
			Первая строка файла
			
			$ echo "Новая строка" > file.txt
			
			$ cat file.txt
			
			Новая строка
			
	  Сравниваем коммиты:
	  
	    Передайте команде git diff хеши обоих коммитов. 
		
		Состояние файлов на момент первого переданного коммита будет 
		
		сравниваться с состоянием файлов на момент второго.
	  
			Пример: (дописали сказку теремок / подселили всех зверей)
			
			$ git log --oneline
			
				70e8b3f (HEAD -> master) Попытался поселить медведя косолапого
				
				fc40ed0 Поселить волчка-серого бочка
				
				ad1d57a Поселить лисичку-сестричку
				
				543a530 Поселить зайчика-побегайчика
				
				365a6eb Поселить лягушку-квакушку
				
				d2a7bbe Поселить мышку-нарушку
				
				7a01cce Исходное состояние теремка
				
			$ git diff 7a01cce 70e8b3f
				
				diff --git a/teremok.txt b/teremok.txt
				
				index f62ab9d..02076a5 100644
				
				--- a/teremok.txt
				
				+++ b/teremok.txt
				
				@@ -1 +1 @@
				
				-Теремок стоит, и в нём: никого нет
				
				\ No newline at end of file
				
				+Теремок развален
				
			___________________________________________________________________________
			
			Вместо 70e8b3f можно было использовать HEAD: git diff 7a01cce HEAD, 
			
			потому что HEAD указывает на последний коммит.
			
			$ git diff 7a01cce HEAD
				
				diff --git a/teremok.txt b/teremok.txt
				
				index f62ab9d..02076a5 100644
				
				--- a/teremok.txt
				
				+++ b/teremok.txt
				
				@@ -1 +1 @@
				
				-Теремок стоит, и в нём: никого нет
				
				\ No newline at end of file
				
				+Теремок развален
				
			___________________________________________________________________________
			
			Если коротко, это сказка о том, как теремок был и его не стало. 
			
			А теперь попробуйте узнать, кто подселялся между лягушкой-квакушкой и волчком — серым бочком. 
			
			Используйте соответствующие хеши коммитов.
			
			$ git diff 7a01cce fc40ed0
				
				diff --git a/teremok.txt b/teremok.txt
				
				index f62ab9d..5cca19b 100644
				
				--- a/teremok.txt
				
				+++ b/teremok.txt
				
				@@ -1 +1,6 @@
				
				-Теремок стоит, и в нём: никого нет
				
				\ No newline at end of file
				
				+Теремок стоит, и в нём:
				
				+Мышка-норушка
				
				+Лягушка-квакушка
				
				+Зайчик-побегайчик
				
				+Лисичка-сестричка
				
				+Волчок-серый бочок
				
14. Игнорирование файлов

	  а) Как заполнить .gitignore
	  
			С точки зрения Git .gitignore — это обычный текстовый файл. 
			
			Его добавляют в корень репозитория и тоже коммитят.
			
			В простейшем случае в .gitignore указывают все файлы, 
			
			которые нужно игнорировать (по одному имени на строку). 
			
			Но часто удобнее использовать шаблоны. Шаблон, или правило, — это способ 
			
			указать сразу на несколько файлов с однотипными названиями.
			
				ВАЖНО!!!
				
				Правила из .gitignore применяются только к новым (untracked) файлам. 
				
				Если файл уже попал в staging area или в коммит, 
				
				то правила на него не распространяются.
				
			- Комментарий
			
				сли строка начинается с #, то это комментарий, 
				
				и .gitignore не будет его учитывать.
				
			- Просто название файла
			
				Допустим, нужно, чтобы Git игнорировал все файлы .DS_Store. 
				
				Для этого достаточно добавить в .gitignore строку с названием файла.
				
			- Звёздочка (*)

				Символ звёздочки (*) соответствует любой строке, включая пустую. 
				
				Если такой символ используется в шаблоне в .gitignore, значит, 
				
				файл будет проигнорирован вне зависимости от того, что будет на месте звёздочки.
				
				//игнорировать все файлы, которые заканчиваются на .jpeg
				
				*.jpeg

				//игнорировать все файлы "tmp" во всех подпапках папки docs
				
				docs/*/tmp 
				
				ВАЖНО!!! 
				
				Если задать правило, которое состоит только из звёздочки, 
				
				Git будет игнорировать все файлы. 
				
				Это происходит потому, что под звёздочку подходит любое имя файла.
				
			- Вопросительный знак (?)
			
				Вопросительный знак ? соответствует одному любому символу.
				
				file?.txt
				
				Если сохранить такую запись в .gitignore, то будут проигнорированы, 
				
				например, файлы fileA.txt и file1.txt. А вот файл file12.txt не будет 
				
				проигнорирован, потому что в его названии два символа после file, а не один.
				
			- Квадратные скобки ([…])
			
				Квадратные скобки, как и вопросительный знак, соответствуют одному символу. 
				
				При этом символ не любой, а только из списка, который указан в скобках.
				
				//игнорировать файлы file0.txt, file1.txt и file2.txt
				
				//при этом не игнорировать file3.txt, file4.txt, ...
				
				file[0-2].txt
				
				В скобках можно либо перечислить символы ([abc]), либо задать диапазон ([a-z]).
				
			- Слеш (/)
			
				Косая черта, или слеш (/), указывает на каталоги. 
				
				Если шаблон в .gitignore начинается со слеша, то Git проигнорирует 
				
				файлы или каталоги только в корневой директории.
				
				//игнорировать todo.txt в корне репозитория
				
				/todo.txt

				//для сравнения: spam.txt будет игнорироваться во всех папках
				
				spam.txt
				
				Теперь файл todo.txt в корневом каталоге будет проигнорирован. 
				
				При этом, например, файл subdir/todo.txt по-прежнему отслеживается.
				
				Если шаблон заканчивается слешем, то правило применится только к папке.
				
				//игнорировать папку build
				
				build/

				Обратите внимание: если build — это папка, то она будет проигнорирована. 
				
				Если build — обычный файл, то он не подпадёт под правило и не будет игнорироваться.
				
			- Парные звёздочки (**)
			
				Функция парных звёздочек (**) похожа на функцию одинарной (*). 
				
				Отличие в том, как они работают с вложенными папками. 
				
				Двойная звёздочка может соответствовать любому количеству таких папок 
				
				(в том числе нулю). Одинарная может соответствовать только одной.
				
				//игнорировать файлы "docs/current/tmp", "docs/old/tmp",
				
				//а также "docs/old/saved/a/b/c/d/tmp"
				
				//и даже "docs/tmp", потому что ноль вложенных папок тоже подходит
				
				docs/**/tmp
				
				
				//игнорировать только "docs/current/tmp" и "docs/old/tmp"
				
				//файл "docs/old/saved/a/b/c/d/tmp" не попадает в правило
				
				docs/*/tmp
				
				ВАЖНО!!!
				
				Для двойной звёздочки верно то же самое, что и для одной: 
				
				если задать правило **, то будут проигнорированы все файлы.
				
			- Восклицательный знак (!)
			
				
				Любое правило в файле .gitignore можно инвертировать с помощью восклицательного знака (!).
				
				//игнорировать все JPEG-файлы
				
				*.jpeg
								
				
				//но только не мем с Doge
				
				!doge.jpeg 
				
				Теперь файл doge.jpeg будет отслеживаться, хотя 
				
				остальные jpeg-файлы будут проигнорированы. Такие правила 
				
				удобны для добавления исключений из других правил .gitignore
				
	  б) git status --ignored 
	  
			Игнорируемые файлы не отображаются в выводе команды git status, 
			
			иначе они бы засоряли вывод.
			
			Если всё же нужно отобразить все игнорируемые файлы, 
			
			то это можно сделать с помощью ключа --ignored: git status --ignored. 
			
			В таком случае в выводе git status появится раздел Ignored files
			
15. Клонировать репозиторий git clone

	  Откройте этот репозиторий. Нажмите на зелёную кнопку Code. 
	  
	  Появится окно со ссылкой. Если вы уже настроили SSH-ключ, 
	  
	  убедитесь что выбрана опция SSH и нажмите на кнопку с двумя квадратами 
	  
	  справа — она скопирует ссылку в буфер обмена. Вы также можете скопировать ссылку вручную.
	  
			ВАЖНО!!! (копировать нужно HTTPS) 
			
			$ git clone https://github.com/yandex-praktikum/git-clone-practice.git

	  Убедитесь в том, что репозитории связаны, командой git remote -v.
	  
			$ cd git-clone-lesson
			
			$ git remote -v
			
			origin    git@github.com:yandex-praktikum/git-clone-lesson.git (fetch)
			
			origin    git@github.com:yandex-praktikum/git-clone-lesson.git (push)

	  Готово! Теперь на вашей машине есть копия удалённого репозитория.
	  
16. Выполняем Fork

	  Допустим, вы хотите усовершенствовать чужой проект или как-то использовать его 
	  
	  в своей работе, но у вас нет прав на изменение оригинального репозитория.
	  
	  В этом уроке разберём ещё одну полезную операцию копирования проектов. 
	  
	  В отличие от клонирования, она не скачает репозиторий на локальный компьютер, 
	  
	  но добавит его прямо в ваш аккаунт на сервере GitHub.

		а) Что такое Fork
		
			Fork (англ. «развилка», «ответвление»), или «форк», — это GitHub-операция; 
			
			напрямую с Git она не связана. «Форк» создаёт копию репозитория в аккаунте GitHub. 
			
			Такая копия будет полностью независима. Изменения, которые вы внесёте, 
			
			не будут синхронизированы с исходным репозиторием.
			
			В процессе «форка» создаётся копия всех файлов, истории коммитов и веток. 
			
			Эта копия сохраняется в вашей учётной записи GitHub.
			
				Применяем Fork
				
				- откройте репозитеорий, который необходимо "Fork-нуть"
				
				- нажмите на кнопку Fork в правом верхнем углу
				
				- В открывшемся окне вы можете поменять название и описание репозитория. 
				
				  Или поставить галку, чтобы склонировать только главную ветку вместо всех сразу. 
				  
				  Нажмите Create fork (англ. **«создать копию репозитория»).
				  
				- Немного подождите, пока репозиторий скопируется. 
				
				  После этого он будет доступен по адресу https://github.com/%USERNAME%/git-basics, 
				
				  где %USERNAME% — ваше имя пользователя.
				
				  В результате вы получите полную копию исходного репозитория, 
				  
				  которую можно свободно изменять и которой можно управлять.
				  
17. Исполнение кода через консоль Git

	  Для исполнения файла со скриптом необходимо: 
	  
	  - Сделать файл исполняемым

			$ chmod +x chek.sh  --  эта команда сделает файл исполняемым
		
	  - Исполнить скрипт
	  
			$ ./check.sh  -- эта команда исполнит скрипт
			
18. Что такое ветка

		Ветка (англ. branch) — это изолированный поток разработки проекта. 
		
		В таком потоке можно проверять разные идеи, тестировать новую функциональность и так далее.
		
		Ветки позволяют экспериментировать с проектом в Git, 
		
		но при этом сохранять репозиторий в стабильном состоянии. 
		
		Каждый член команды может работать в своей ветке и не мешать другим: 
		
		коммиты, которые он сделает, не будут видны из других веток. 
		
		А когда работа будет доделана, ветки можно соединить.
		
		Ветки полезны, даже если вы работаете в одиночку — например, над сайтом. 
		
		Прежде чем писать новую функциональность, для неё следует создать отдельную ветку. 
		
		Также ветки позволяют одному человеку переключаться между несколькими задачами сразу.
		
			Просмотреть ветки проекта — git branch
			
				$ git branch 
				
				* master # мы в основной ветке

				"чтобы выйти из просмотра веток, может понадобиться Q!"

				При вызове git branch выводятся ветки, которые есть в проекте. 
				
				Звёздочкой (*) отмечено, в какой ветке вы находитесь в текущий момент.
				
19. Создаём ветку

		git branch <название ветки>
		
			ВАЖНО!!!
			
			В названии ветки есть слеш — что это значит?
			
			Название ветки в Git может состоять из букв, цифр, а также включать любой 
			
			из четырёх символов: ., -, _, /. Эти символы не несут особого смысла. 
			
			Например, ветка feature/add-branch-info могла бы называться feature_add-branch-info 
			
			или feature-add-branch. Обратите внимание, что ветки не образуют иерархии, 
			
			как директории, разделённые символом /.
			
		$ git branch feature/add-branch-info -- создали ветку feature/add-branch-info

		$ git branch -- посмотрели ветки
  
		feature/add-branch-info -- появилась новая

		* master                     
		
		* значит, что мы находимся в основной ветке 
		
		Готово! Сейчас в вашем репозитории две ветки — основная и feature/add-branch-info.
		
		
		Как назвать новую ветку
		
		Есть разные подходы к наименованию веток. Каждая команда разработки выбирает свой. 
		
		Но независимо от подхода ветки нужно называть так, чтобы другим участникам было понятно, 
		
		что в них происходит.
		
20. Переключиться на другую ветку — git checkout

		Чтобы начать работу в feature/add-branch-info, перейдите в неё с помощью команды 
		
		git checkout с флагом — названием ветки: git checkout feature/add-branch-info.
		
			$ git checkout feature/add-branch-info # перешли в новую ветку

				Switched to branch 'feature/add-branch-info'

			$ git branch # проверили

				* feature/add-branch-info # теперь находимся тут
  
				  master
				
			Строчка Switched to branch... (англ. «переключено на ветку…») сообщает, 
			
			на какую ветку вы только что переключились.
			
	Создать ветку и сразу переключиться на неё — git checkout -b <название_ветки>
	
		Можно создать ветку и сразу начать в ней работать. За это отвечает команда 
		
		git checkout с флагом -b (от англ. branch) и названием ветки. 
		
		Эта команда делает то же самое, что и последовательность команд 
		
		git branch %название-ветки% && git checkout %название-ветки%.

			$ git checkout -b bugfix/fix-branch # создали ветку и сразу на неё переключились

				Switched to a new branch 'bugfix/fix-branch'

			$ git branch

				* bugfix/fix-branch # сразу в нужной ветке

				feature/add-branch-info

				master
						
	На какой коммит указывает bugfix/fix-branch
	
		Ветка в Git — это указатель на коммит. Когда вы делаете новый коммит в ветке, 
		
		этот указатель передвигается вперёд. Пока вы не вносили новые коммиты в ветку bugfix/fix-branch, 
		
		поэтому она указывает на тот же коммит, что и основная ветка. 
		
		Убедитесь в этом с помощью команды git log --oneline.
		
			$ git checkout bugfix/fix-branch

			$ git log --oneline

				a7eb909 (HEAD -> bugfix/fix-branch, master) Добавить файл README

			$ git checkout feature/add-branch-info

			$ git log --oneline

				abd591c (HEAD -> feature/add-branch-info) Добавить git branch и git checkout в README

				a7eb909 (master, bugfix/fix-branch) Добавить файл README
				
21. Сравниваем ветки

		Используйте команду git diff main feature/diff (или git diff master feature/diff), 
		
		чтобы вывести разницу между двумя ветками. Вы увидите точно такой же вывод, 
		
		как если бы сравнивали два коммита между собой.
		
			$ git diff master feature/diff # сравнили ветки master и feature/diff

				diff --git a/README.md b/README.md

				index 58151f3..28e2619 100644

				--- a/README.md

				+++ b/README.md

				@@ -1,2 +1,3 @@

				"Ветки в Git"

				git branch - посмотреть все активные ветки

				+Для сравнения веток есть команда git diff
				
		При сравнении вы также можете использовать название ветки и хеш коммита. 
		
		Для этого сначала выполните команду git log --oneline, чтобы вывести список коммитов.
		
		Теперь выполните команду git diff с названием основной ветки и хешем коммита в ветке 
		
		feature/diff. У нас получилась следующая комбинация: $ git diff master db2798c.
		
			$ git diff master db2798c

				"вывод будет такой же, как при использовании git diff main feature/diff"
				
		Вывод будет такой же, как после выполнения команды git diff main feature/diff. 
		
		Когда вы вызываете git diff <название_ветки1> <название_ветки2>, Git находит два коммита, 
		
		на которые указывает каждая из веток, и сравнивает их. Также с веткой можно сравнивать указатель HEAD.
		
22. Суффикс навигации ~

		Сравнивать хеши комитов может быть неудобно, ведь в одной ветке их может быть много. 
		
		Представьте: сначала вы выводите историю через git log, затем ищете в длинном списке хеши тех коммитов, 
		
		которые хотите сравнить, и только потом выполняете git diff. Для облегчения этой задачи в Git есть 
		
		суффикс навигации ~N, где N — это число. Он отсчитывает от заданного коммита N коммитов назад во времени. 
		
		Нумерация начинается с нуля: commit~0 — это сам коммит, commit~1 — предыдущий, 
		
		commit~2 — предшествующий предыдущему и так далее. Например, HEAD~1 — это следующий за текущим коммит. 
		
		А main~5 — это пятый коммит в ветке main, если считать с последнего выполненного коммита.
		
		На практике чаще нужен либо текущий коммит (HEAD), либо следующий за ним (HEAD~1). 
		
		Для ~1 есть специальное сокращение ~ (без числа). То есть вместо HEAD~1 обычно пишут просто HEAD~.
		
		Также можно использовать ~0, но большого смысла в этом нет: main~0 — это то же самое, 
		
		что просто main, а HEAD~0 — это просто HEAD.
		
23. Слияние ветки

		git merge <название_ветки> -- слияние ветки
		
			Перед тем как начать процесс слияния, нужно перейти в ветку, куда должны добавиться изменения. 
			
			Обычно это главная ветка. Перейдите в неё и вызовите команду git merge с именем присоединяемой 
			
			ветки feature/diff в качестве параметра.
			
				$ git checkout master -- переключились на главную ветку
			
				$ git merge feature/diff -- объединили ветки
				
					Updating 79122ec..db2798c
				
					Fast-forward
				
					README.md | 1 +
				
					1 file changed, 1 insertion(+)
					
				Объединение веток прошло успешно! 
				
				Все коммиты из feature/diff добавлены в главную ветку. В сообщении после слияния содержится следующая информация:
				
					Updating 79122ec..db2798c — значит, что коммиты c 79122ec по db2798c были объединены.
					
					Fast-forward — это режим слияния. Fast-forward (англ. «перемотка») значит, что итогом слияния будет линейная история коммитов. 
					
					Такое происходит, когда истории двух веток находятся на одной прямой — то есть когда одна ветка продолжает историю, начатую другой, 
					
					как в нашем примере.
					
					Информация о конкретных изменениях. В нашем примере поменялся файл README.md (1 file changed): 
					
					в нём теперь одна новая строчка (1 insertions(+)).
					
			Основная ветка и feature/diff теперь указывают на один коммит. 
			
			Вы можете проверить это с помощью git log --oneline.
			
			До слияния	$ git log --oneline
					
							db2798c (HEAD -> feature/diff) Добавить git diff в README
							
							79122ec (master) Добавить git branch в README
							
							24e65ed (bugfix/fix-branch) Добавить файл README
					
				____________________________________________________________________
				
			После       $ git log --oneline
					
							db2798c (HEAD -> master, feature/diff) Добавить git diff в README
							
							79122ec Добавить git branch в README
							
							24e65ed (bugfix/fix-branch) Добавить файл README
							
			Откройте файл README.md и убедитесь, что теперь он содержит информацию из обеих веток.
			
				$ cat README.md
					
					// Ветки в Git
					
					git branch - посмотреть все активные ветки
					
					Для сравнения веток есть команда git diff
					
24. Удалить ветку после объединения

		git branch -D <название_ветки>  -- удаление ветки после объединения
		
			После того как произошло слияние, ветку-донора можно удалить. 
			
			Для этого в основной ветке введите команду git branch с флагом -D 
			
			от англ. delete — «удалить») и названием ветки.
			
			$ git branch  --  проверяем местоположение
				
				bugfix/fix-branch
				
				feature/add-branch-info
				
				feature/diff

				* master
				
			$ git checkout master  --  если не в основной, переходим в неё

			$ git branch -D feature/diff  --  удаляем поглощаемую ветку

				Deleted branch feature/diff (was db2798c).
				
			Ветка feature/diff удалена — об этом говорит сообщение Deleted branch feature/diff.
			
		ВАЖНО!!!
		
		  Если в момент удаления вы будете находиться в той ветке, которую хотите удалить, 
		
		Git сообщит об ошибке: can not delete branch (англ. «не получается удалить ветку»).
		
		  У команды git branch -D есть более безопасный вариант с флагом -d. 
		
		Он удалит ветку только если она была полностью объединена с другой — то есть если две ветки стали 
		
		(или изначально были) частью одной истории. Например, если вы нечаянно создали ветку с неправильным названием, 
		
		её можно удалить через git branch -d %имя_ветки%.
		
		  Удаление локальной ветки через Git не удаляет ветку на GitHub!

25. Что такое конфликт

		Когда сразу несколько членов команды работают над одним и тем же фрагментом проекта в 
		
		разных ветках, при слиянии могут происходить конфликты. Рассмотрим, как это бывает и 
		
		что делать в такой ситуации.
		
		Знакомьтесь: конфликт
		
			Допустим, вы решили отредактировать параграф текста и исправить опечатки. 
			
			В этот момент ваш коллега поменял тот же самый параграф в соседней ветке 
			
			change/github-info и влил изменения в master.
			
			После завершения работы вы делаете финальный коммит в своей ветке edit/fix-typoes, 
			
			переходите в основную и пытаетесь выполнить слияние. Но в терминале появляется такое сообщение.
			
				$ git commit -m "Исправить опечатки" && git checkout main
				
				$ git merge edit/fix-typoes
				
					Auto-merging pages/table-of-content.txt   --   тут Git самостоятельно внёс изменения 
					
					CONFLICT (content): Merge conflict in github.txt   --   здесь возник конфликт
					
					Automatic merge failed; fix conflicts and then commit the result   --   слияния не произошло
					
			Если Git не может провести слияние изменений автоматически, он сообщает о конфликте. 
			
			Конфликт — это ситуация, в которой один или несколько человек модифицировали один и тот же файл. 
			
			При этом результаты таких модификаций оказались несовместимы и разобраться в том, 
			
			какой из вариантов правильный, может только человек.
			
			В разработке, например, конфликты чаще всего возникают, когда несколько 
			
			программистов одновременно меняют код в одном и том же месте.
			
		Как разрешать конфликты: общие рекомендации
		
			Во время слияния Git сам подсвечивает файлы, которые не смог объединить. 
			
			Чтобы разобраться в ситуации, нужно сделать следующее:
			
				- Заглянуть в файл, где произошёл конфликт.
				
				- Изучить обе стороны конфликта — вашу версию и версию вашего коллеги. 
				
				Ваша задача — правильно собрать две версии в итоговую, так чтобы изменения 
				
				обеих сторон не потерялись. Новая версия станет текущей актуальной.
				
				- Вручную удалить или подправить неактуальные изменения, если они есть.
				
				- Подготовить изменения к сохранению и сделать коммит.
				
			Подробнее о том, как работать с конфликтами, мы ещё расскажем дальше в курсе. 
			
			Также узнать об этом больше можно из официальной документации Git.
			
26. 