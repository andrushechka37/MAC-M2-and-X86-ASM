# Как дебагать из вскода?
# Устанавливаем расширение "clangd"
![31](/images/31.png)
# Чтобы ставить breakpointы ставим расширение asm-enable-debug а еще ставим CodeLLDB
![31](/images/35.png)
![31](/images/36.png)
# Прописываем в launch.json 
```
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "lldb",
      "request": "launch",
      "name": "noob debug",
      "program": "${workspaceFolder}/a.out",
      "args": [],
      "cwd": "${workspaceFolder}"
    }
  ]
}
```
# Отключаем все расширения, которые используют IntelliSense, потому что они конфилтуют с clangd
# Нажимаем clangd: Download language server
![31](/images/32.png)
# Нажимаем clangd: Manually activate extension
![31](/images/33.png)
# Нажимаем clangd: Restart language server
![31](/images/34.png)
# Прописываем в консоль
`bear -- make`
# Еще раз прописываем restart, должна появится папка .cache и файл compile_commands.json

# Как запускать?
# Переходим сюда
![31](/images/38.png)
# Нажимаем зеленую кнопочку play и дебаг выполнится до breakpointа
![31](/images/39.png)
# Дебагаем как обычно через кнопочку