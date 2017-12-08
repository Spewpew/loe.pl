## loe.pl Возможности
* Инициализация базового GNU Autotools проекта
* Функции чтения параметров из командной строки и/или файла (INI)
* SDL2: Создание архивов(например с данными для игр) во время компиляции
  * Функции загрузки из архива текстур, музыки, данных о хитбоксах https://github.com/Spewpew/boxy
* Стек, списки
## Что требуется
* indent - https://www.gnu.org/software/indent/ , 2.2.11
* gperf  - https://www.gnu.org/software/gperf/ , 3.1
* darc   - https://github.com/Spewpew/darc , 1.0
* Perl   - https://www.perl.org , 5.26.1
* base-devel(autoconf,automake,gcc,m4,pkg-config, итд...)
### Создаём новый проект
    loe.pl --create-project=projname[,TOKENLIBSANDCFLAGS:PKGCONFIG_NAME[,...]]
#### Пример
    loe.pl --create-project=sdlgame,SDL2:sdl2,SDL2_IMAGE:SDL2_image,SDL2_MIXER:SDL2_mixer
* Создаётся директория **sdlgame** со следующим содержимым
  * configure.ac
  * src/loe.pl
  * src/Makefile.am.shadow
  * Makefile.am
  * src/main.loe.pl.c
  * src/configure.ac.shadow
  * src/Makefile.am
#### Устанавливаем компоненты GNU Build System
    cd sdlgame
    autoreconf -i
#### Что дальше?
    mkdir debug
    cd debug
    ../configure --prefix=$PWD/install CFLAGS="-g -O0" --enable-shadow
    make
На основе файла **src/main.loe.pl.c** будет сгенерирован файл **debug/src/main.c**
#### Что делает --enable-shadow?
При создании архива для распространения ```make dist``` будет использоваться сгенерированный файл **debug/src/main.c**. Следы loe будут потеряны :sob:.
### Подробности по мере роста интереса
