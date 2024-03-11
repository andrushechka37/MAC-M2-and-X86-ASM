# Покупаем сервер

### Регистрируемся на сайте [тут](https://timeweb.cloud)
### Покупаем сервер такого плана
![7](/images/7.png)
### Скачиваем расширение на vscode ()картинка
![8](/images/8.png)

## Подключаем сервер

![9](/images/9.png)
connect to host-> add new ssh host->вводим ssh, он подключатеся

заходим в host

вводим пароль с сайта картинка


apt install g++
apt install nasm
apt install lldb
apt install make 


## пример кода и мейкфайла:
C
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
```
section .text

global hui                ; predefined entry point name for ld

hui:       mov rax, 0x01      ; write64 (rdi, rsi, rdx) ... r10, r8, r9
            mov rdi, 1         ; stdout
            mov rsi, Msg
            mov rdx, MsgLen    ; strlen (Msg)
            syscall
            
            ret
            
section     .data
            
Msg:        db "__Hllwrld", 0x0a
MsgLen      equ $ - Msg
```

Make:
```Makefile
.Phony print: main.o 1-nasm.o
	ld -s -o main.o 1-nasm.o -o main

main.o: main.c
	gcc -no-pie main.c main.o

1-nasm.o: 1-nasm.s
	nasm -f elf64 -l 1-nasm.lst 1-nasm.s
```




-------------------------------------------------
---------------------------------
------------


-----------------------
------------------------------
------------------------------
-------------------------------
--------------------------
-----------------

-----------------------
------------------------------
------------------------------
-------------------------------
--------------------------
-----------------

-----------------------
------------------------------
------------------------------
-------------------------------
--------------------------
-----------------

-----------------------
------------------------------
------------------------------
-------------------------------
--------------------------
-----------------





























# Как слинковать *.c и *.s для X86 на mac m2

### Нужно установить brew
place holder install brew

### Прописываем эту команду в терминале, чтобы установить nasm
[источник](https://github.com/orgs/Homebrew/discussions/3526)
 
```brew install nasm```

### Прописываем это, чтобы установить brew для mac X86
```arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"```



### Прописываем это, чтобы создать псевдоним для скачанного brew, чтобы он не путался с оригинальным
``` alias ibrew='arch -x86_64 /usr/local/bin/brew'```

### Прописываем это, чтобы установить gcc для X86


```ibrew install gcc```
# Компилляция и линковка

### Объектый для *.c
```arch -x86_64 gcc -c NAME.c```

### Объектный для *.s
```nasm -f macho64 NAME.s```

### Линковка в исполняемый файл

``` arch -x86_64 gcc your_object_files_compiled_with_gcc -o main```


# Дебаг через консоль:

* заходим в директорию проекта
* ```lldb RUN_FILE_NAME```
* ```b main```
* ```run```
* ```s``` to step next

# Важно!!!!!!!!! В мейн файле .c использовать ```exit(0)``` вместо ```return 0```



# Это не надо читать и делать, это просто описание моих похождений
# Дебаг не через консоль это ебаный пиздец! оно вам реально не надо
![5](/images/5.png)

## Варианты:
* Сертифицировать скачанный gdb(не получилось)
  
   [источник](https://dev.to/jasonelwood/setup-gdb-on-macos-in-2020-489k)

* Поставить ghidra и использовать lldb 
  


  [два сайт](https://www.reddit.com/r/ghidra/comments/t0dmqm/debug_libldb_java_missing_macos/0)


* Ставим гидру   [как тут](https://lachy.io/articles/properly-installing-ghidra-on-an-m1-mac)

она ставится сама в /opt/homebrew/Caskroom

gradle ставится сюда сама /opt/homebrew/Cellar
писать ниче не надо, это подсказка

## запуск гидры
```cd /opt/homebrew/Caskroom/ghidra/11.0.1-20240130/ghidra_11.0.1_PUBLIC/```
```./ghidraRun```

Получаем ошибку:
java.lang.RuntimeException: Agent terminated with error: no lldb in java.library.path: 
/Users/anzhiday/Library/Java/Extensions:/Library/Java/Extensions:/Network/Library/Java/Extensions:/System/Library/Java/E
xtensions:/usr/lib/java:.
liblldb not found - add relevant java.library.path to support/launch.properties
no lldb-java in java.library.path: 
/Users/anzhiday/Library/Java/Extensions:/Library/Java/Extensions:/Network/Library/Java/Extensions:/System/Library/Java/E
xtensions:/usr/lib/java:.
libl...SBDebugger_eBroadcastBitProgress_get(Native Method)
	at SWIG.SBDebugger.<clinit>(SBDebugger.java:478)
	at agent.lldb.lldb.DebugClientImpl.createClient(DebugClientImpl.java:45)
	at agent.lldb.manager.impl.LldbManagerImpl.lambda$start$0(LldbManagerImpl.java:483)
	at agent.lldb.gadp.impl.LldbClientThreadExecutor.init(LldbClientThreadExecutor.java:50)
	at agent.lldb.gadp.impl.AbstractClientThreadExecutor.run(AbstractClientThreadExecutor.java:95)
	at java.base/java.lang.Thread.run(Thread.java:1583)
---------------------------------------------------
Build Date: 2024-Jan-30 1212 EST
Ghidra Version: 11.0.1
Java Home: /Library/Java/JavaVirtualMachines/microsoft-21.jdk/Contents/Home
JVM Version: Microsoft 21.0.2 


## Настройка lldb

```/Users/anzhiday/Downloads/ghidra_11.0.1_PUBLIC/Ghidra/Debug/Debugger-swig-lldb```

тут нужно запустить sh скрипт

разрешаем изменения

![1](/images/1.png)


![2](/images/2.png)
![3](/images/3.png)
![4](/images/4.png)

```xattr -d com.apple.quarantine ./macos_debugger_lldb_build_from_brew.sh```

заходим в этот ебучий файл 
/Users/anzhiday/Downloads/ghidra_11.0.1_PUBLIC/Ghidra/Debug/Debugger-swig-lldb

и меняем 
пишем поеботу без пробелов ебатб ахуеть

```GHIDRA_INSTALL_DIR='/opt/homebrew/Caskroom/ghidra/11.0.1-20240130/ghidra_11.0.1_PUBLIC'```

  [лучше полностью посмотреть инструкцию](https://fossies.org/linux/ghidra/Ghidra/Debug/Debugger-swig-lldb/InstructionsForBuildingLLDBInterface.txt)



выполняем эту хуйню

./macos_debugger_lldb_build_from_brew.sh



билд суккесфул нахуй блядь 5 утра нахуй

теперь мы получаем новую ошибку, которую я не знаю как фиксить



java.util.concurrent.ExecutionException: java.util.concurrent.TimeoutException java.lang.RuntimeException: java.util.concurrent.ExecutionException: java.util.concurrent.TimeoutException at ghidra.debug.api.target.Target$ActionEntry.get(Target.java:121) at ghidra.debug.api.target.Target$ActionEntry.run(Target.java:104) at ghidra.app.plugin.core.debug.gui.control.TargetActionTask.run(TargetActionTask.java:33) at ghidra.util.task.Task.monitoredRun(Task.java:134) at ghidra.util.task.TaskRunner.lambda$startTaskThread$0(TaskRunner.java:106) at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144) at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642) at java.base/java.lang.Thread.run(Thread.java:1583) Caused by: java.util.concurrent.ExecutionException: java.util.concurrent.TimeoutException at java.base/java.util.concurrent.CompletableFuture.reportGet(CompletableFuture.java:396) at java.base/java.util.concurrent.CompletableFuture.get(CompletableFuture.java:2073) at ghidra.debug.api.target.Target$ActionEntry.get(Target.java:118) ... 7 more Caused by: java.util.concurrent.TimeoutException at java.base/java.util.concurrent.CompletableFuture$Timeout.run(CompletableFuture.java:2920) at java.base/java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:572) at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:317) at java.base/java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:304) ... 3 more --------------------------------------------------- Build Date: 2024-Jan-30 1212 EST Ghidra Version: 11.0.1 Java Home: /Library/Java/JavaVirtualMachines/microsoft-21.jdk/Contents/Home JVM Version: Microsoft 21.0.2 OS: Mac OS X 14.3.1 aarch64

Telegram: @azhkov

Может полезные ссылки

https://github.com/NationalSecurityAgency/ghidra/issues/4035
https://github.com/NationalSecurityAgency/ghidra/issues/6095
