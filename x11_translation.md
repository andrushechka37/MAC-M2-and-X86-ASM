# Как прокидывать X11 трансляцию на мак для сервака

# Устанавливает sfml
`sudo apt-get install libsfml-dev`
# Устанавливаем xauth
`apt install xauth`
# настраиваем хуету от сюда
[вот это](https://www.businessnewsdaily.com/11035-how-to-use-x11-forwarding.html)

# Качаем кварц из файла [XQuartz-2.7.11.dmg](/XQuartz-2.7.11.dmg)

# Пишем это
`defaults write org.macports.X11 enable_iglx -bool true`

[two](https://unix.stackexchange.com/questions/429760/opengl-rendering-with-x11-forwarding)

# Запускаем через иконку кварц
`ssh -X -v root@90.156.208.69`
# Пишем пароль

# Тест:
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

 [хуй](/Readme.md)



 ##### Секретный гайд как использовать copy/paste в окне xquartz
 ##### Прописываем настройки
 ![31](/images/41.png)
 ![31](/images/42.png)
 ##### Вставлять через `option + клик мыши`
