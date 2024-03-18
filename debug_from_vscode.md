# Как дебагать из вскода?
# Устанавливаем расширение "clangd" - нужный нам языковой сервер
![31](/images/31.png)
# Чтобы ставить breakpointы ставим расширение asm-enable-debug, а для самого дебага -- CodeLLDB
![31](/images/35.png)
![31](/images/36.png)
# Прописываем в launch.json вот это, если у вас нет этого файла, то в папке .vscode создайте его, если папки нет, создайте папку
## Мб нужнна фул папка вскод
![31](/images/71.png)

```JSON
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "lldb",
      "request": "launch",
      "name": "noob debug",
      "program": "${workspaceFolder}/a.out", // <-- захардкоженный исполняемый файл, который надо дебажить
      "args": [],
      "cwd": "${workspaceFolder}"
    }
  ]
}
```




# Отключаем все расширения, которые используют IntelliSense, потому что они конфилтуют с clangd
## а именно нажимаем кнопку disable у расширений в кнопке расширений
![31](/images/72.png)
# Нажимаем clangd: Download language server (shift + command + P)
![31](/images/32.png)
# Нажимаем clangd: Manually activate extension
![31](/images/33.png)
# Нажимаем clangd: Restart language server
![31](/images/34.png)

# Прописываем в консоль
`sudo apt install bear`

`bear -- make -B -j`
# Нажимаем clangd: Restart language server
![31](/images/34.png)


# Появится папка .cache и файл compile_commands.json

# Нажимаем clangd: Restart language server
![31](/images/34.png)

`bear -- make -B -j`

# Как комплиллировать?

# Вы должны собирать проект через Makefile!
# Лучше всего собирать аналогично примеру, иначе работоспобность не гарантируется

```MAKEFILE
.Phony print: printf.o main.c
	clang-14 -no-pie -g -O0 main.c printf.o && ./a.out

printf.o: printf.s
	nasm -f elf64 -g -l printf.lst printf.s
```


# Как запускать?

# Переходим сюда
![31](/images/38.png)
# Нажимаем зеленую кнопочку play и дебаг выполнится до breakpointа
![31](/images/39.png)

