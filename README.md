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

\- untracked (не отслеживаемый) – в рабочей директории, но нет ни в одной версии HEAD / Git не знает о файле)

\- modified (изменен) – в рабочей директории есть более новая версия по сравнению с HEAD / изменения не находятся в следующем commit

\- staged (подготовлен) - готов к commit

6.  Просмотр изменений

   git log

7. Удаленный репозиторий

   а) необходимо создать новый репозиторий в GitHub

         \- даем имя (как имя папки)

         \- выбираем public / private

         \- создаем

   б) связываем удаленный репозиторий на GitHub с локальным, на компьютере Git

         \- генерируем SSH-ключ (сетевой протокол Secure Shell Protocol)

                Приватный ключ (Только для вас. Хранится на вашем компьютере. Используется для расшифровки данных)

                Публичный ключ (Доступен всем и используется для расшифровки данных)

                     ls  -la .ssh/ (проверяет наличие ключей)

                     ls  -a ~/.ssh (проверяет наличие ключей)

          \- привязываем SSH-ключ к GitHub

          \- связываем удаленный и локальный репозиторий

            git remote add origin git@github.com:%ИМЯ АККАУНТА%/ИМЯ ПРОЕКТА.git

            origin – имя удаленного репозитория (по умолчанию)

            ИМЯ АККАУНТА (URL) – копируем со страницы удаленного репозитория

          \- убедиться, что репозитории связаны

            git remote  -v