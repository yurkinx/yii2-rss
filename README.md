yii2-feed
=========

Yii2 Framework extension to provide functionality for consuming RSS and Atom feeds using zend-feed library.

Installation
------------
```code
{
	"require": 
	{
  		"yurkinx/yii2-feed": "dev-master"
	}
}
```
Configuration
-------------
In config file
```code
/config/web.php
```
Add image component
```code
'components' => array(
        ...
        'feed' => array(
        	 	'class' => 'yii\feed\FeedDriver',
        		),
		    )
```
Simple usage
-----
Read Rss feed:
```php
$feed=Yii::$app->feed->reader()->import('http://exapmple.com/feed.rss');
```
This will get RSS feed, parse it and return feed object.
For more details you can read the official Zend-feed extention documentaion:
http://framework.zend.com/manual/1.12/en/zend.feed.reader.html

Write Rss feed:
```php
$feed=Yii::$app->feed->writer();
$feed->setTitle('Paddy\'s Blog');
$feed->setLink('http://www.example.com');
$feed->setFeedLink('http://www.example.com/atom', 'atom');
$feed->addAuthor(array(
		    'name'  => 'Paddy',
		    'email' => 'paddy@example.com',
		    'uri'   => 'http://www.example.com',
		));
$feed->setDateModified(time());
$feed->addHub('http://pubsubhubbub.appspot.com/');
		 
/**
* Add one or more entries. Note that entries must
* be manually added once created.
*/
$entry = $feed->createEntry();
$entry->setTitle('All Your Base Are Belong To Us');
$entry->setLink('http://www.example.com/all-your-base-are-belong-to-us');
$entry->addAuthor(array(
		    'name'  => 'Paddy',
		    'email' => 'paddy@example.com',
		    'uri'   => 'http://www.example.com',
		));
$entry->setDateModified(time());
$entry->setDateCreated(time());
$entry->setDescription('Exposing the difficultly of porting games to English.');
$entry->setContent(
		    'I am not writing the article. The example is long enough as is ;).'
);
$feed->addEntry($entry);
/**
* Render the resulting feed to Atom 1.0 and assign to $out.
* You can substitute "atom" with "rss" to generate an RSS 2.0 feed.
*/
$out = $feed->export('atom');
echo $out;
```
Take a look at Zend-feed writer official documentaion for more advanced usage
http://framework.zend.com/manual/1.12/en/zend.feed.writer.html 
