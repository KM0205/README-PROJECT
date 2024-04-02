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
			
12. 
	