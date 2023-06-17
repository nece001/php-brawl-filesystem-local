# php-brawl-filesystem-local
php 本地（硬盘）文件系统基础服务适配项目

# 示例

```php
    $conf = array(
        'base_path' => 'D:\Work\temp\test',
        'sub_path' => 'a/b',
        'base_url' => 'http://aaa.com',
    );

    $config = FileSystemFactory::createConfig('Local');
    $config->setConfig($conf);

    $fso = FileSystemFactory::createClient($config);
    try {

        $fso->write('c/' . time() . '.txt', 'test');
        $fso->append('c/' . time() . '.txt', 'test');

        $fso->copy('a/b/c/1687011074.txt', 'a/1.txt');
        $fso->move('a/b/a/1.txt', 'a/2.txt');
        $fso->upload('a/b/a.txt', 'a/3.txt');

        var_dump($fso->exists('a/b/c/1687011074.txt'));
        echo $fso->read('a/b/c/1687011074.txt');
        $fso->delete('a/b/a/1.txt');

        $fso->mkDir('a/d');
        echo $fso->lastModified('a/b/c/1687011074.txt');
        echo $fso->fileSize('a/b/c/1687011074.txt');
        
        print_r($fso->readDir('a/b/c/'));

        echo $fso->getUri(), '<br>';
        echo $fso->getUrl();
    } catch (Throwable $e) {
        echo $e->getMessage(), '<br>';
        echo $fso->getErrorMessage();
    }
```