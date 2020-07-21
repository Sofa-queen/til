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
