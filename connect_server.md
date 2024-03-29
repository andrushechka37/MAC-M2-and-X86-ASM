# Как подключить сервер к маку на M2 для компилляции x86 программ
# Этап 1: Покупаем сервер

# Регистрируемся на сайте [тут](https://timeweb.cloud/r/vf23262)
![10](/images/10.png)
# Заходим в вкладку "Облачные серверы"
![10](/images/11.png)
# Выбирираем систему
![10](/images/25.png)
# Ниже выбираем конфигурацию
![10](/images/26.png)
# В итоге получается сервер такого плана
> [!CAUTION]
> ### бэкапы по желанию
> ### Никакие другие настройки можно не трогать
![7](/images/7.png)
----------------
----------------
----------------
----------------
----------------
----------------
----------------
----------------
----------------
# Этап 2: Скачиваем расширение на vscode
![8](/images/9.png)
----------------
----------------
----------------
----------------
----------------
----------------
----------------
----------------
----------------

# Этап 3: Подключаем сервер
# Нажимаем на эту синюю кнопку
![9](/images/8.png)

# В появившемся окне нажимаем на "Connect to host" или ее альтернативу на русском языке
![8](/images/13.png)

# Нажимаем "Add New SSH Host"
![8](/images/14.png)
# Далее нам нужно вставить туда наш ssh адрес который мы берем отсюда
## Чтобы найти ssh ключ заходим на сайт, нажимаем на сервер
![8](/images/15.png)
# Копируем адрес
![8](/images/16.png)

# Вводим ssh в предлагаемое поле

# Будут предложены настройки конфигов, выбираем самый первый
![10](/images/27.png)
# Опять подключаемся к узлу через кнопку и Connect to host
![9](/images/8.png)

# Жмем на появившиеся цифирки
![9](/images/17.png)

# Будет выведено новое окно, жмем 'продолжить'

![21](/images/21.jpg)

# Прописываем пароль root в следующем окне, берем его отсюда
![9](/images/18.png)

# Для более удобного управления сервером можно скачать приложение как на компьютер, так и на телефон.
## Для этого необходимо нажать на соответствущую кнопку, как показано на рисунке ниже.

![](images/download_app.png)

## Cервер можно безопасно
+ ### останавливать
![](images/stop_server.png)
+ ### запускать
![](images/run_server.png)

#### P.S. Во время остановки стоимость аренды меньше)

# Тест:



## Устанавливаем gcc и nasm
```
apt install gсс
apt install nasm
```

## Создаем 1-nasm.s
```
section .text

global hui                ; predefined entry point name for ld

hui:        mov rax, 0x01      ; write64 (rdi, rsi, rdx) ... r10, r8, r9
            mov rdi, 1         ; stdout
            mov rsi, Msg
            mov rdx, MsgLen    ; strlen (Msg)
            syscall
            
            ret
            
section     .data
            
Msg:        db "__Hllwrld", 0x0a
MsgLen      equ $ - Msg
```

## Создаем main.c
```C
#include <stdio.h>
#include <stdlib.h>

extern void hui();

int main() {
    printf("\n>>> main(): start\n\n");

    int a = 85, b = 14;

    hui();

    printf("\n<<< main(): end\n\n");
    return 0;
}
```
## И пишем в консоль

`nasm -f elf64 -l 1-nasm.lst 1-nasm.s`

`gcc -no-pie main.c 1-nasm.o`

`./a.out`
## Должно вывести это


![9](/images/20.png)
