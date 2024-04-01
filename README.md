## Homework

### Part I
1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
   - Создан репозиторий на сервисе github.com
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
   - Создан файл README.md
3. Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;.
---
   ```
   #include <iostream>
   
   using namespace std;

   int main() {
     cout << "Hello world";
     return 0;
   }
   ```
---
5. Добавьте этот файл в локальную копию репозитория.
   - ```$ git add hello_world.cpp```
6. Закоммитьте изменения с *осмысленным* сообщением.
   - ```$ git commit -m"Create_Hello_world"```
7. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение "Hello world from @name", где "@name" имя пользователя.
---
   ```
   #include <iostream>

   using namespace std;
   
   int main() {
     string name = "";
     cin >> name;
     cout << "Hello world from " << name;
     return 0;
   }
   ```
---
9. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
   - ```$ git commit -m"Hello_world and name```
   >Git add - эта команда создаёт новый блоб с новым содержимым. Она обновляет запись в индексе для hello_world.cpp с указанием на новый блоб.
10. Запуште изменения в удалёный репозиторий.
   - ```$ git push origin main```
11. Проверьте, что история коммитов доступна в удалёный репозитории.
   - ```$ git log``` или посмотреть на самом гитхабе историю коммитов
---
   ```
      commit 3fee8423885caaa11600132775bd66e3ad0d928d (HEAD -> main, origin/main, origin/HEAD)
      Author: z1qnezt <misha232dog@gmail.com>
      Date:   Mon Apr 1 16:22:15 2024 +0300

    Hello_world and name

      commit 339edaec1add74a16d1386553a03e74d44aa51fa
      Author: z1qnezt <misha232dog@gmail.com>
      Date:   Mon Apr 1 16:20:53 2024 +0300

    Create_Hello_world

      commit ffbe10a298e1ab9690d113dce612d79352e00b8f
      Author: _Twent <76701971+z1qnezt@users.noreply.github.com>
      Date:   Mon Apr 1 16:19:34 2024 +0300

    Initial commit
   ```
---

### Part II

1. В локальной копии репозитория создайте локальную ветку `patch1`.
   - ```$ git branch patch1```
   - ```$ git switch patch1```
2. Внесите изменения в ветке **patch1** по исправлению кода и избавления от *using namespace std;*.
---
   ```
   #include <iostream>
   
   int main() {
     std::string name = "";
     std::cin >> name;
     std::cout << "Hello world from " << name;
     return 0;
   }
   ```
---
4. **commit**, **push** локальную ветку в удалённый репозиторий.
   - ```$ git add .```
   - ```$ git commit -m"HelloWorld edited"```
   - ```$ git push origin patch1```
5. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
   - Шаг выполнен
6. Создайте pull-request `patch1 -> main`.
   - Шаг выполнен
7. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
---
   ```
   #include <iostream>
   
   int main() {
     std::string name = ""; // name
     std::cin >> name; // input
     std::cout << "Hello world from " << name; // output
     return 0;
   }
   ```
---
9. **commit**, **push**.
   - ```$ git add .```
   - ```$ git commit -m"EditHelloWorld+Username+Comments"```
   - ```$ git push origin patch1```
10. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
   - Шаг выполнен
11. В удалённый репозитории выполните  слияние PR `patch1 -> main` и удалите ветку `patch1` в удаленном репозитории.
   - Шаг выполнен
11. Локально выполните **pull**.
    - ```$ git pull origin patch1```
12. С помощью команды **git log** просмотрите историю в локальной версии ветки `main`.
    - ```$ git log```
---
   ```
      commit 8df45162f894f927dca112aba891663e56e69f95 (HEAD -> patch1, origin/patch1)
      Author: z1qnezt <misha232dog@gmail.com>
      Date:   Mon Apr 1 16:26:54 2024 +0300

    HelloWorld addComments

      commit 185045b0c4ad75c3e81343838577931964dcaa00
      Author: z1qnezt <misha232dog@gmail.com>
      Date:   Mon Apr 1 16:24:59 2024 +0300

    HelloWorld edited

      commit 3fee8423885caaa11600132775bd66e3ad0d928d (origin/main, origin/HEAD, main)
      Author: z1qnezt <misha232dog@gmail.com>
      Date:   Mon Apr 1 16:22:15 2024 +0300

    Hello_world and name

      commit 339edaec1add74a16d1386553a03e74d44aa51fa
      Author: z1qnezt <misha232dog@gmail.com>
      Date:   Mon Apr 1 16:20:53 2024 +0300

    Create_Hello_world
    
      commit ffbe10a298e1ab9690d113dce612d79352e00b8f
      Author: _Twent <76701971+z1qnezt@users.noreply.github.com>
      Date:   Mon Apr 1 16:19:34 2024 +0300

    Initial commit
   ```
---
12. Удалите локальную ветку `patch1`.
    - ```$ git branch -D patch1```

### Part III

1. Создайте новую локальную ветку `patch2`.
   - ```$ git branch patch2```
   - ```$ git switch patch2```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
   - ```$ clang-format -style=Mozilla hello_world.cpp```
---
   ```
#include <iostream>

int
main()
{
  std::string name = "";                    // name
  std::cin >> name;                         // input
  std::cout << "Hello world from " << name; // output
  return 0;
}
   ```
---
3. **commit**, **push**, создайте pull-request `patch2 -> main`.
   - ```$ git add -A```
   - ```$ git commit -m "Clang"```
   - ```$ git push origin patch2```
   - PR создан
4. В ветке **main** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
---
   ```
   #include <iostream>

   int main() {
     std::string name = ""; // UserName
     std::cin >> name; // Input
     std::cout << "Hello world from " << name; // Output
     return 0;
   }

   ```
---
5. Убедитесь, что в pull-request появились *конфликтны*.
    - Шаг выполнен, конфликты присутсвуют
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
    - ```$ git pull --rebase origin main```
---
   ```
    remote: Enumerating objects: 8, done.
    remote: Counting objects: 100% (8/8), done.
    remote: Compressing objects: 100% (4/4), done.
    remote: Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (4/4), 1.79 KiB | 367.00 KiB/s, done.
    From https://github.com/z1qnezt/lab02
    * branch            main       -> FETCH_HEAD
    3fee842..99a2c79  main       -> origin/main
    Auto-merging hello_world.cpp
    CONFLICT (content): Merge conflict in hello_world.cpp
    error: could not apply 45cb76a... Clang
    hint: Resolve all conflicts manually, mark them as resolved with
    hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
    hint: You can instead skip this commit: run "git rebase --skip".
    hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
    Could not apply 45cb76a... Clang
   ```
---
   - ```$ git rebase --continue```
---
   ```
   [detached HEAD 45cb76a] mozilla codestyle rebase
 1 file changed, 7 insertions(+)
Successfully rebased and updated refs/heads/patch2.
   ```
---
7. Сделайте *force push* в ветку `patch2`
    - ```$ git push origin patch2 --force```
---
   ```
   Enumerating objects: 6, done.
   Counting objects: 100% (6/6), done.
   Delta compression using up to 8 threads
   Compressing objects: 100% (4/4), done.
   Writing objects: 100% (4/4), 2.70 KiB | 2.70 MiB/s, done.
   Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
   remote: Resolving deltas: 100% (1/1), completed with 1 local object.
   To https://github.com/z1qnezt/lab02.git
    + 3fee842...99a2c79 patch2 -> patch2 (forced update)
   ```
---
8. Убедитель, что в pull-request пропали конфликтны.
    - Шаг выполнен, конфликты пропали
9. Вмержите pull-request `patch2 -> main`.
    - Шаг выполнен
10. Проверка
    - ```$ g++ hello_world.cpp -o hello_world```
    файл приложен к репозиторию
