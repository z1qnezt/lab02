## Homework

### Part I
1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
   - Создан репозиторий на сервисе github.com
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
   - Создан файл README.md и .gitignore
3. Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;.
   ```
   #include <iostream>
   
   using namespace std;

   int main() {
     cout << "Hello world";
     return 0;
   }
   ```
4. Добавьте этот файл в локальную копию репозитория.
   - ```$ git add hello_world.cpp```
5. Закоммитьте изменения с *осмысленным* сообщением.
   - ```$ git commit -m"Create_Hello_world"```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение "Hello world from @name", где "@name" имя пользователя.
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
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
   - ```$ git commit -m"Hello_world+username"```
   >Git add - эта команда создаёт новый блоб с новым содержимым. Она обновляет запись в индексе для hello_world.cpp с указанием на новый блоб.
8. Запуште изменения в удалёный репозиторий.
   - ```$ git push origin main```
9. Проверьте, что история коммитов доступна в удалёный репозитории.
   - ```$ git log``` или посмотреть на самом гитхабе историю коммитов

### Part II

1. В локальной копии репозитория создайте локальную ветку `patch1`.
    - ```$ git branch patch1```
2. Внесите изменения в ветке **patch1** по исправлению кода и избавления от *using namespace std;*.
   ```
   #include <iostream>
   
   int main() {
     std::string name = "";
     std::cin >> name;
     std::cout << "Hello world from " << name;
     return 0;
   }
   ```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
   - ```$ git add .```
   - ```$ git commit -m"EditHelloWorld+Username"```
   - ```$ git push origin patch1```
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
   - Шаг выполнен
5. Создайте pull-request `patch1 -> main`.
   - Шаг выполнен
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
   ```
   #include <iostream>
   
   int main() {
     std::string name = ""; // созлание переменной
     std::cin >> name; // считывание
     std::cout << "Hello world from " << name; // вывод
     return 0;
   }
   ```
7. **commit**, **push**.
   ```
   - $ git add .
   - $ git commit -m"EditHelloWorld+Username+Comments"
   - $ git push origin patch1
   ```
9. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
   - Шаг выполнен
10. В удалённый репозитории выполните  слияние PR `patch1 -> main` и удалите ветку `patch1` в удаленном репозитории.
   - Шаг выполнен
11. Локально выполните **pull**.
   - ```$ git pull origin patch1```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `main`.
   - ```$ git log```
   - Шаг выполнен
12. Удалите локальную ветку `patch1`.
   - ```$ git branch -d patch1```

### Part III

1. Создайте новую локальную ветку `patch2`.
   - ```$ git branch patch1```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
```
   - $ clang-format -style=mozilla -dump-config > .clang-format
   - $ clang-format -i *.cpp
```
3. **commit**, **push**, создайте pull-request `patch2 -> main`.
```
   - $ git add .
   - $ git commit -m"Update hello_world.cpp"
   - $ git push origin patch2
   - PR создан
```
4. В ветке **main** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
   ```
   #include <iostream>
   
   int main() {
     std::string name = ""; // Созлание переменной.
     std::cin >> name; // Считывание.
     std::cout << "Hello world from " << name; // Вывод.
     return 0;
   }
   ```
5. Убедитесь, что в pull-request появились *конфликтны*.
    - Шаг выполнен, конфликты присутсвуют
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
    - ```$ git pull --rebase origin main```
   ```
   From https://github.com/z1qnezt/lab02
    * branch            main       -> FETCH_HEAD
   Auto-merging hello_world.cpp
   CONFLICT (content): Merge conflict in hello_world.cpp
   error: could not apply 2b4e68f... CLang
   hint: Resolve all conflicts manually, mark them as resolved with
   hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
   hint: You can instead skip this commit: run "git rebase --skip".
   hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
   Could not apply 2b4e68f... CLang
   ```
    - ```$ git rebase --continue```
   ```
   Successfully rebased and updated refs/heads/patch2.
   ```
7. Сделайте *force push* в ветку `patch2`
    - ```$ git push origin patch2 --force```
   ```
   Enumerating objects: 6, done.
   Counting objects: 100% (6/6), done.
   Delta compression using up to 8 threads
   Compressing objects: 100% (4/4), done.
   Writing objects: 100% (4/4), 2.70 KiB | 2.70 MiB/s, done.
   Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
   remote: Resolving deltas: 100% (1/1), completed with 1 local object.
   To https://github.com/z1qnezt/lab02.git
    + 2b4e68f...46c0e7e patch2 -> patch2 (forced update)
   ```
8. Убедитель, что в pull-request пропали конфликтны.
    - Шаг выполнен, конфликты пропали
9. Вмержите pull-request `patch2 -> main`.
    - Шаг выполнен
