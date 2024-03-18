# Как прокидывать X11 трансляцию на мак для сервака + sfml

# Устанавливаем sfml 
# Здесь и далее прописываем все на сервере
`sudo apt-get install libsfml-dev`
# Устанавливаем xauth -- плагин под управлением Bukkit, создающий внутрисерверную регистрацию пользователям.
`apt install xauth`

# Сначала прописываем это
` vim /etc/ssh/sshd_config`

# И выставляем параметры как тут
```
UsePAM yes

#AllowAgentForwarding yes
#AllowTcpForwarding yes
#GatewayPorts no
X11Forwarding yes
X11DisplayOffset 10
X11UseLocalhost yes
#PermitTTY yes
PrintMotd no
#PrintLastLog yes
#TCPKeepAlive yes
#PermitUserEnvironment no
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS no
#PidFile /run/sshd.pid
#MaxStartups 10:30:100
#PermitTunnel no
#ChrootDirectory none
#VersionAddendum none
```
# Выйти :q

`systemctl restart ssh.service`

`sudo apt install x11-apps`




# Качаем кварц из файла на мак[XQuartz-2.7.11.dmg](/XQuartz-2.7.11.dmg)

# Reebotаем мак + выход из пользователя

# Пишем это в маковском терминале
`defaults write org.macports.X11 enable_iglx -bool true`

# Отрываем в launchpadе приложение xqauatz
## Нажимаем на иконку


# Заходим в терминал с английской раскладкой!!! иначе после входа на сервер не будет работать клава

## Терминал может сам не открыться, поэтому открываем вручную
![ч](/images/74.png)
![ч](/images/75.png)
## Откроется такое окно
![ч](/images/76.png)

# В него прописываем в него команду вида
# Ваши цифирки берем отсюда
![v](/images/81.png)

`ssh -X -v root@90.156.208.69`

# Вводим пароль 
# Проверка на на работоспособность:

# Прописываем в консоль терминала xquartz

`xeyes`

# Должно создать такое окно:
![v](/images/82.png)

# X11 трансляция настроена!







# Тест sfml:
```C++
#include <SFML/Graphics.hpp>

int main()
{
    sf::RenderWindow window(sf::VideoMode(200, 200), "SFML works!");
    sf::CircleShape shape(100.f);
    shape.setFillColor(sf::Color::Green);

    while (window.isOpen())
    {
        sf::Event event;
        while (window.pollEvent(event))
        {
            if (event.type == sf::Event::Closed)
                window.close();
        }

        window.clear();
        window.draw(shape);
        window.display();
    }

    return 0;
}
```

# Компиллирование
```g++ sfml_example.cpp -o sfml_example -lsfml-graphics -lsfml-window -lsfml-system```

`LIBGL_ALWAYS_INDIRECT=1 ./sfml_example`
# Источники:

find / -name "xauth"
 sudo apt install vim
 vim /etc/ssh/sshd_config
 systemctl restart ssh.service
 printenv | grep DISPLAY
 brew install --cask xquartz
 service sshd restart
 apt install xeyes
 service iptables stop
 LIBGL_ALWAYS_INDIRECT=1 ./sfml_example



 ##### Секретный гайд как использовать copy/paste в окне xquartz
 ##### Прописываем настройки
 ![31](/images/41.png)
 ![31](/images/42.png)
 ##### Вставлять через `option + клик мыши`



[вот это](https://www.businessnewsdaily.com/11035-how-to-use-x11-forwarding.html)
[two](https://unix.stackexchange.com/questions/429760/opengl-rendering-with-x11-forwarding)