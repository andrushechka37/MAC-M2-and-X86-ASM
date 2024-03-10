# Как слинковать *.cpp и *.s для X86 на mac m2

## Нужно установить brew
## Установка nasm

```brew install nasm```

## Установка gcc для mac x 86:
[источник](https://github.com/orgs/Homebrew/discussions/3526)

### Установка brew для mac X86
```arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"``` 

### Псевдоним для скачанного brew, чтобы он не путался с оригинальным
``` alias ibrew='arch -x86_64 /usr/local/bin/brew'```

### Установка gcc для X86
```ibrew install gcc```
-------------------------------------------------------------------------------------------------------------
## Как запускать
### Объектый для *.c
```arch -x86_64 gcc -c haha.cpp```

### Объектный для *.s
```nasm -f macho64 func.s```

### Компилляция в исполняемый файл

``` arch -x86_64 gcc your_object_files_compiled_with_gcc -o main```
# Дебаг через консоль:
просто lldb

# Дебаг не через консоль это ебаный пиздец!

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


Telegram: @azhkov

Может полезные ссылки
https://github.com/NationalSecurityAgency/ghidra/issues/4035
https://github.com/NationalSecurityAgency/ghidra/issues/6095