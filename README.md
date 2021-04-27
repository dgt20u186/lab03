# lab03
## Далгатов Гитиномагомед
**Задание 1.** 
  Вам поручили перейти на систему автоматизированной сборки **CMake**. Исходные файлы находятся в директории formatter_lib. В этой директории находятся файлы для      статической библиотеки *formatter*. Создайте ```CMakeList.txt``` в директории formatter_lib, с помощью которого можно будет собирать статическую библиотеку *formatter*.
  
  Команда 1: ```$ git clone https://github.com/tp-labs/lab03```
  
  Вывод 1:
  ```
  Клонирование в «lab03»…
  remote: Enumerating objects: 91, done.
  remote: Counting objects: 100% (3/3), done.
  remote: Compressing objects: 100% (3/3), done.
  remote: Total 91 (delta 0), reused 0 (delta 0), pack-reused 88
  Распаковка объектов: 100% (91/91), 1.03 MiB | 1.72 MiB/s, готово.
  ```
  
  Команда 2:
  ```
  $ cat > CMakeLists.txt <<EOF
  > cmake_minimum_required(VERSION 2.8)
  > add_library(formatter STATIC formatter.h formatter.cpp)
  > EOF
  ```
  
  Команда 3: ```$ cmake ~/dgt20u186/workspace/tasks/lab03/formatter_lib```
  
  Вывод 3(фрагмент): 
  ```
  -- Configuring done
  -- Generating done
  -- Build files have been written to: /home/dgt20u186/dgt20u186/workspace/tasks/lab03/formatter_lib
  ```
  
  Команда 4: ```make```
  
  Вывод 4(фрагмент):
  ```
  Scanning dependencies of target formatter
  [ 50%] Building CXX object CMakeFiles/formatter.dir/formatter.cpp.o
  [100%] Linking CXX static library libformatter.a
  [100%] Built target formatter
  ```
  
**Задание 2.**
  У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием ```CMakeList.txt``` для статической библиотеки *formatter*, ваш руководитель поручает заняться созданием ```CMakeList.txt``` для библиотеки *formatter_ex*, которая в свою очередь использует библиотеку *formatter*.
  
  Командa 1: ```cp -r formatter_lib formatter_ex_lib/```
  
  Командa 2:
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

  1. Команда 1: ```$ mv formatter_ex_lib/ hello_world_application/```
  
     Команда 2:
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
    
     Команда 3: ```$ cmake ~/dgt20u186/workspace/tasks/lab03/hello_world_application```
     
     Вывод 3:
     ```
     -- Configuring done
     -- Generating done
     -- Build files have been written to: /home/dgt20u186/dgt20u186/workspace/tasks/lab03/hello_world_application
     ```
     Команда 4: ```make```
     
     Вывод 4:
     ```
     Scanning dependencies of target hello_world
     [ 83%] Building CXX object CMakeFiles/hello_world.dir/hello_world.cpp.o
     [100%] Linking CXX executable hello_world
     [100%] Built target hello_world
     ```
     
  2. Команда 1:  
     ```
     $ cat > CMakeLists.txt <<EOF
     > cmake_minimum_required(VERSION 3.4) 
     > add_library(solver_lib STATIC solver.h solver.cpp)
     > EOF
     ```
     
     Команда 2: ```cmake ~/dgt20u186/workspace/tasks/lab03/solver_lib```
     
     Вывод 2(фрагмент):
     ```
     -- Configuring done
     -- Generating done
     -- Build files have been written to: /home/dgt20u186/dgt20u186/workspace/tasks/lab03/solver_lib
     ```
     
     Команда 3: ```make```
     
     Команда 4: ```$ mv solver_lib/ formatter_ex_lib/```
     
     Команда 5:
     ```
     $ cat > CMakeLists.txt <<EOF
     > cmake_minimum_required(VERSION 3.4)
     > project(solver)
     > add_executable(solver equation.cpp)
     > include_directories(formatter_ex_lib)
     > add_subdirectory(formatter_ex_lib)
     > include_directories(solver_lib)
     > add_subdirectory(solver_lib)
     > target_link_libraries(solver formatter_ex)
     > target_link_libraries(solver solver_lib)
     > EOF
     ```
     
     Команда 6: ```$ cmake ~/dgt20u186/workspace/tasks/lab03/solver_application```
     
     Вывод 6:
     ```
     -- The C compiler identification is GNU 9.3.0
     -- The CXX compiler identification is GNU 9.3.0
     -- Check for working C compiler: /usr/bin/cc
     ```
     
     
     
