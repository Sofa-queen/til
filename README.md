#today I`ve learned

14.07.20.
1) Научилась искать нужный темплейт в magento с помощью команды: bin/magento dev:template-hints:enable || bin/magento dev:template-hints:disable .
(bin/magento list - для просмотра всех команд в magento) 
2) Научилась добавлять новую переменную в сессию .

15.07.20.
1) Узнала, что если шаблон, прописанный в структуре xml файла,  не отображается на странице, следует посмотреть файл блока, который относится к этому шаблону ( в нём может быть логика, которая не выполняется или препятствует выводу ) . 
2) Узнала, что если надо переписать функцию, которая обращается к родительскому классу, с помощью preference, нужно исследовать этот класс и переписать функцию без использования parent::имя_функции .

16.07.20
1) Получила полезную информацию об отмене последнего коммита в github :
   Если вы не опубликовали свои изменения :
   git commit -a --amend     -    позволяет добавить к последнему коммиту новые изменения .
   git reset --soft HEAD^    -    отменяет последний коммит, но изменения, которые вы внесли, сохранятся .
   git reset --hard HEAD^    -    удаляет последний коммит и все правки, которые не были закоммиченны .
   
   Если изменения опубликованы надо сделть коммит отмены коммита : 
   git revert commit-sha1    и    git push .

20.07.20
1) Научилась получать значения из таблицы core_config_data : 
 в агрументе конструктора использовать \Magento\Framework\App\Config\ScopeConfigInterface $scopeConfig и 
 установить свойство класса : $this->scopeConfig = $scopeConfig ;

 Для получения значения конфигурации использовать :
   $this->scopeConfig->getValue('dev/debug/template_hints', \Magento\Store\Model\ScopeInterface::SCOPE_STORE);

2) Узнала, как создать новые поля конфигурации в System.xml файле. Чтобы посмотреть, как это выглядит необходимо пройти Store->Setting->Configuration.3) Узнала, что такое ajax и как его использовать в js. Пример:
    $('.class').click(function(){
        $.ajax({
            url: 'http://bugtracking.com/create.php',
            method: 'POST',
            data: {
                name: 'yasha',
                login: 'cat'
            },
            success: function(result){
                console.log(result);
            },
            error: function(error){
                console.log(error.status);
            }
        });
    });
 
4) Столкнулась с проблемой /var/run/mysqld/mysqld.sock (mysql сервер не может подключиться к Unix-сокету) .
   Решение : sudo killall -9 mysqld  
             sudo /etc/init.d/mysql start

             sudo mkdir /var/run/mysqld
             sudo mkfifo /var/run/mysqld/mysqld.sock
             sudo chown -R mysql /var/run/mysqld

21.07.20.
1) Получилось выводить отмеченные продукты в боковую панель wishlist, но не факт, что правильно .

22.07.20.
1) Научилась перенаправлять пользователя на предыдущую страницу.
2) Сделала плагин, который добавляет продукты из гостевого списка желаний в wishlist по customer_id, после того, как пользователь вошёл в систему.
3) Узнала, что у каждого типа клиента есть предпочтительный метод аутентификации.

23.07.20.
1) Чтобы при git push не запрашивались пароль и имя пользователя, необходимо переключить удаленные URL-адреса с HTTPS на SSH:
   git remote -v    
                   origin  https://hostname/USERNAME/REPOSITORY.git (fetch)
                   origin  https://hostname/USERNAME/REPOSITORY.git (push)

   git remote set-url origin git@hostname:USERNAME/REPOSITORY.git
2) Узнала, что такое cron в magento и для чего нужен .

24.07.20.
1) Записать массив в log файл : $this->logger->log(100,print_r($data,true));

27-29.07.20.
1) Закончила работу с cron. Каждый день в полночь будет запускаться код, который выберет все wishlist c customer_id равным нулю и удалит те, которые были не активны на протяжении времени, определенного через админку. 
2) Начала работать над добавлением продуктов из гостевого списка желаний в wishlist покупателя после его регистрации, когда необходимо подтверждать свою электронную почту.
3) Научилась работать с датами, вычислять разницу между ними.
4) Научилась получать выборочные данные из таблиц бд.

30.07.20.
1) Установила mailhog: 
   sudo apt-get -y install golang-go
   go get github.com/mailhog/MailHog

   Запуск:
   ~/go/bin/MailHog

2) Столкнулась с проблемой:
   E: Не удалось получить файл блокировки /var/lib/dpkg/lock-frontend - open (11: Ресурс временно недоступен)
   E: Невозможно получить блокировку внешнего интерфейса dpkg (/var/lib/dpkg/lock-frontend); она уже используется другим процессом?

   Научилась ее решать:
   sudo fuser -v /var/lib/dpkg/lock
   sudo fuser -vki /var/lib/dpkg/lock
   sudo dpkg --configure -a

   Усли не помогло:
   sudo rm /var/lib/dpkg/lock
   sudo dpkg --configure -a

   Или закрыть вкладку терминала с установкой, либо перезагрузить комп и выполнить : 
   sudo dpkg --configure -a 

3) Установила mhsendmail: 
   go get github.com/mailhog/mhsendmail
   ln  ~/go/bin/mhsendmail /usr/local/bin/mhsendmail
   В /etc/php/7.2/fpm/php.ini ( sudo service php7.2-fpm restart )  ,  /etc/php/7.2/cli/php.ini : 
      sendmail_path = /usr/local/bin/mhsendmail
   
   Проверка:
   php -a
   php > mail('test@test.com', 'test', 'test');

   или 
 
   mhsendmail test@mailhog.local <<EOF
   From: App <app@mailhog.local>
   To: Test <test@mailhog.local>
   Subject: Test message

   Some content!
   EOF

31.07.20.
1) Научилась делать дамп бд :
mysqldump -u имя_пользователя -p имя_базы_данных > путь_и_имя_файла_дампа
2) Чтобы сделать текст в magento переводимым на другие языки :
         <?= __('<your_string>') ?>
https://devdocs.magento.com/guides/v2.4/frontend-dev-guide/translations/translate_theory.html

3.08.20.
1) Решение проблемы nginx: [emerg] no port in upstream "fastcgi_backend" in /var/www/html/magento/nginx.conf.sample:52
   в начало файла /
   etc/nginx/sites-available/magento добавить :
           upstream fastcgi_backend {
                       server   unix:/var/run/php/php7.3-fpm.sock;
           }
        
2) Решение проблемы ERROR 1045 (28000): Access denied for user 'root'@'localhost' :
         sudo apt-get remove --purge mysql-server mysql-client mysql-common
         sudo apt-get autoremove
         sudo apt-get autoclean
         sudo apt install mysql-server
         
         sudo mysql -u root
         DROP USER 'root'@'localhost';
         CREATE USER 'root'@'%' IDENTIFIED BY '';
         GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
         FLUSH PRIVILEGES;
3) Узнала, что 502 ошибка может возникнуть, если неправильно указать путь к php7.3-fpm.sock файлу ...((((
4) При ошибки, возникающей при работе с .vimrc :
      Неизвестная функция: plug#begin / Это не команда редактора: Plug 'dense-analysis/ale'
   Выполнить команду :
      curl -fLo ~/.vim/autoload/plug.vim --create-dirs  https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
       
4.08.20.
1) Генерация нового ключа SSH и добавление его в ssh-agent 
    https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
2) Вы можете проверить синтаксис файлов конфигурации Nginx, выполнив:
   nginx -t -c /etc/nginx/nginx.conf 
3) При nginx: [emerg] bind() to [::]:80 failed (98: Address already in use) выполнить : sudo service apache2 stop

5.08.20.
1) Проблемы с установкой и удалением MySQL в Ubuntu.
   Попробуйте выполнить чистку, а затем переустановите : 
              sudo apt-get remove --purge mysql-\*
              sudo apt-get install mysql-server mysql-client
              
6.08.20.
1) Узнала, что в mysql запросах можно использовать функцию datediff(), например :
   select datediff(now(), updated_at), wishlist.* from wishlist WHERE datediff(now(), updated_at);
2) Столкнулась с проблемой в magento из-за прав.. итог - при установке magento не забыть добавить своего пользователя в группу, дать необходимые права.
   sudo adduser www-data yasha
   sudo usermod -a -G www-data yasha
3) Столкнулась с ошибкой : Call to a member function create() on null in . Она вызвана тем, что $this->wishlistFactory->create() возвращает null, т.к. родительский и дочерний классы имели разные методы __construct.
(дочерний класс не наследовал родительский метод, решение: ипользовать parent:: или писать construct только в дочернем классе).

7.08.20.
1) vendor/bin/phpcs --standard=Magento2 app/code/MyAwesomeExtension
   vendor/bin/phpcbf --standard=Magento2 app/code/MyAwesomeExtension
2) Узнала, что в Magento 2 есть несколько методов защиты шаблона:
   $block->escapeHtml()
   $block->escapeQuote()
   $block->escapeUrl()
   $block->escapeXssInUrl()

17.08.20.
1) Узнала, что такое индексы в magento, для чего используются и как работают.

18.08.20.
1) vim для работы с двумя окнами:
       :vsplit - чтобы расположить две панели рядом
       Ctrl+w+команда - перемещение между окнами 
       :e filename - чтобы открыть другой файл
       :set scrollbind - включить прокрутку 
       
21.08.20.
1) Когда поднимаешь проект на локалке, не забывать изменить value в core_config_data на свой url.

16.09.20.
1) ошибка Not a git repository (or any of the parent directories): .git    -    выполнить git init
2) ошибка при composer install file_put_contents(/home/yash/.composer/auth.json): failed to open stream: Permission denied   -   выполнить  sudo chown -R $USER ~/.composer/
3) ошибка при composer install Uncaught Error: Undefined class constant 'PRE_COMMAND_RUN' возникает из-за устаревшей версии composerhttps://github.com/magento/magento2/issues/27867
