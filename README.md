# lab03
## Далгатов Гитиномагомед
**Задание 1.** 
  Вам поручили перейти на систему автоматизированной сборки **CMake**. Исходные файлы находятся в директории formatter_lib. В этой директории находятся файлы для      статической библиотеки *formatter*. Создайте ```CMakeList.txt``` в директории formatter_lib, с помощью которого можно будет собирать статическую библиотеку *formatter*.
  Команды: 
  ```
  $ cat > CMakeLists.txt <<EOF
  > cmake_minimum_required(VERSION 2.8)
  > add_library(formatter STATIC formatter.h formatter.cpp)
  > cmake ~/workspace/projects/lab03/formatter_lib/
  > 
  > EOF
  ```

**Задание 2.**
  У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием ```CMakeList.txt``` для статической библиотеки *formatter*, ваш руководитель поручает заняться созданием ```CMakeList.txt``` для библиотеки *formatter_ex*, которая в свою очередь использует библиотеку *formatter*.
  Команды:
  ```
  $ cat > CMakeLists.txt <<EOF
  > cmake_minimum_required(VERSION 2.8)
  > project(formatter_ex)
  > include_directories(formatter_lib)
  > add_subdirectory(formatter_lib)
  > add_library(formatter_ex STATIC formatter_ex.h formatter_ex.cpp)
  > target_link_libraries(formatter_ex formatter)
  > EOF
  ```
  
**Задание 3.**
  Конечно же ваша компания предоставляет примеры использования своих библиотек. Чтобы продемонстрировать как работать с библиотекой *formatter_ex*, вам необходимо создать два ```CMakeList.txt``` для двух простых приложений:

+   ```hello_world```, которое использует библиотеку *formatter_ex*;
+   ```solver```, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

  Команды:
  ```
  $ cat > CMakeLists.txt <<EOF
  > cmake_minimum_required(VERSION 2.8)
  > project(hello_world)
  > include_directories(formatter_ex_lib)
  > add_subdirectory(formatter_ex_lib)
  > add_executable(hello_world hello_world.cpp)
  > target_link_libraries(hello_world formatter_ex)
  > EOF
  ```
