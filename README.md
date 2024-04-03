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
      
	  git log -- oneline
	  
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
				
14. 		
	