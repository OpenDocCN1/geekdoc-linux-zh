
## Caching Engines

If you decide to use memcached permanently, make sure you add the command to start memcached to whatever startup facilities or script you prefer, so it loads automatically every time the machine boots.

Now that you’ve got the memcache daemon running, you need to prepare PHP to use the caching system. Download the memcached PECL module from http://pecl.php.net/package/memcache.

Extract the archive and move into the new directory:

```
tar -xzvf memcache-1.4.tgz
cd memcache-1.4
```

Run *phpize*, and then configure and make the DSO:

```
phpize
./configure
make
```

Install the module, as root:

```
make install
```

Finally, add the following line to your php.ini, and restart Apache:

```
extension="memcache.so"
```

## Using memcached

In order to use memcached, the PHP DSO you installed provides the following methods for the Memcache object:

- Memcache::add
  `bool Memcache::add ( string key, mixed var [, int flags [, int expire]] )`
  This method adds a variable or object into memory cache, identified by the token *key*. If a value with the same *key* already exists in the memory cache, *FALSE* is returned. If you want to compress the value to be stored before putting it into the memory cache, supply *MEMCACHE_COMPRESSED* as the flag, otherwise it can be omitted or set to 0. Any value provided for *expire* tells memcached when it should be removed from the cache. A value of 0 for *expire* indicates that the value should be cached indefinitely.
  Only variables and objects can be stored in the memory cache, whereas resources cannot.

- Memcache::close
  `bool Memcache::close ( void )`
  This method closes any non-persistent connection to the memcached server. If an error occurs when closing the connection, *FALSE* is returned.

- Memcache::connect
  `bool Memcache::connect ( string host [, int port [, int timeout]])`
  This method creates and opens a connection to a memcached server running on host. The port parameter specifies the TCP port used by memcached, the default being 11211, and timeout specifies how long to wait when attempting to connect before returning FALSE. Returns true on success, FALSE on failure.

- Memcache::decrement
  `int Memcache::decrement ( string key [, int value])`
  When storing a simple numeric value in the memory cache, you can actually use the decrement() method to decrease the value matching key by the provided value. If no decrement value is specified, the cached value is decremented by 1. This method returns FALSE on failure, or the item’s new value upon success.

- Memcache::delete
  `bool Memcache::delete (string key [, int timeout])`
  This method deletes the item identified by key from the memory cache. Providing a value for timeout causes the item to be deleted after the provided number of seconds. Returns FALSE on failure, and TRUE on success.

- Memcache::flush
  `bool Memcache::flush ( void )`
  This method tells memcached to immediately set the expiration on all items in the cache. Once this method is called, any item in the cache can be overwritten by new keys, but the memory is not released until that happens. This method returns TRUE on success, or FALSE on failure.

- Memcache::get
  `string Memcache::get ( string key )`
  `string Memcache::get ( array keys )`
  This method retrieves an item or items stored in the memory cache, matching the given key or array of keys. It returns either a string or array on success, depending on how many keys were provided to match against, and FALSE if no keys are found matching the input parameters.

- Memcache::getStats
  `array Memcache::getStats ( void )`
  This returns an array containing various bits of information regarding the status of the memory cache, such as current and total connections, number of cached items, and server uptime.

- Memcache::getVersion
  `string Memcache::getVersion ( void )`
  This returns a simple string with the version number of the memcached server, or FALSE if an error occurs.

- Memcache::increment
  `int Memcache::increment ( string key [, int value] )`
  Like the decrement() method, increment() allows you to easily change a simple numeric value directly in the memory cache —in this case, incrementing the stored variable by value, or 1 if no value is provided. Returns the new value on success, or FALSE on failure.

- Memcache::pconnect
  `bool Memcache::pconnect ( string host [, int port [, int timeout]] )`
  This method creates and opens a persistent connection to the memcached server, similar to a MySQL persistent connection. The parameters are the same as connect(): host specifies the memcached server hostname or IP address, port specifies the listening port for memcached, and timeout specifies the connection timeout period.

- Memcache::replace
  `bool Memcache::replace ( string key, mixed var [, int flag [, int expire]] )`
  This searches through the cached objects for an item matching key, and if found, replaces it with the value var. Like add() and set(), replace() can supply a flag to request compression when storing the value, and also give an optional expiration time for the new value. This method returns TRUE on success, FALSE on failure.

- Memcache::set
  `bool Memcache::set ( string key, mixed var [, int flag [, int expire]] )`
  This stores the value var in the memory cache, even if there is a preexisting item matching key. Arguments are identical to those of add() and replace(). Returns TRUE on success, FALSE on failure.

You can use these methods in a similar manner as the MySQLi methods —you connect to the memcached server, process data in and out of the cache, and then disconnect. The following simple example stores a Circle object in the memory cache:

```php
<?php

class Circle
{
    public $radius;
    public function area()
    {
        return pi() * pow($this->radius, 2);
    }
}

$memc = new Memcache();
$memc->connect('10.0.0.20', 11211);

$c = new Circle();
$c->radius = 15;

$memc->set('circel', $c);

$stats = $memc->getStats();

$memc->close();

print_r($stats);
?>
```

If you run this script, it will print an array containing the statistics of the memory cache at that time. If it's the first time you run the script, or first time memcached is used on your server, your curr_items value should be 1, reflecting the newly added Circle object.

```
Array
(
    [pid] => 1379
    [uptime] => 4148
    [time] => 1124758570
    [version] => 1.1.12
    [rusage_user] => 0.030000
    [rusage_system] => 0.010000
    [curr_items] => 1
    [total_items] => 8
    [bytes] => 77
    [curr_connections] => 1
    [total_connections] => 9
    [connection_structures] => 2
    [cmd_get] => 0
    [cmd_set] => 8
    [get_hits] => 0
    [get_misses] => 0
    [bytes_read] => 605
    [bytes_written] => 1856
    [limit_maxbytes] => 134217728
)
```

## Removing memcached

Like the other DSO caching solutions, you can quickly disable memcache functionality by commenting-out or removing the appropriate lines from php.ini and restarting Apache. At that point you can delete memcache.so from your PHP extensions directory, and the memcached daemon from the system binary folder (wherever it was installed to earlier, most likely /usr/local/bin or /usr/bin).

## Using Different Caching Engines Together

Now at this point, the gears might be turning in your head, and you start to wonder, “What happens if I used more than one caching engine simultaneously?” Well, as you might suspect, a proper choice of complementary solutions can slightly increase performance, but there are certain combinations that won't do you any good.

JPCache and memcached can play well with others, but APC, eAccelerator, and the Zend Optimizer are somewhat mutually exclusive. While they might load together just fine, and not throw any errors when executing a PHP script, there’s little to no reason to use a combination of opcode caches. All three in some way or another provide roughly the same functionality, so using multiple opcode caches will only result in the system being as fast as the slowest cache.

Try to pick just one opcode caching solution, and try combining it with memcached and JPCache. Throw your preferred content-compression solution into the mix — the built-in content compression in JPCache is still too buggy — and you’ve got a lean and mean combined-cache serving machine.

## Choosing Your Caching Engine

So which caching solution is right for you? Perhaps it’s best for you to first evaluate the needs of your system, and look for any places that are currently or will soon be a bottleneck. If you’re struggling with heavy classes and objects zinging around your scripts, or frequently pull a large amount of repetitive data from your database, memcached will be your best bet for some performance improvements. If your website code generates relatively static pages — you’re not using excessive user personalization or other highly dynamic elements — you should consider using JPCache. If the data layer is not really your bottleneck, but your PHP code could use some general performance tweaks, one of the opcode caching engines will help you out. If you’re unsure which optimizer / cache to use, a safe bet would be APC. What it may lack in the low-level engine boost or optimization at Zend Optimizer may deliver, it makes up for by being highly customizable, and well-supported — it is after all, part of the PECL repository.

## Summary

Regardless of which caching solution you choose, any of the systems discussed in this chapter have the potential to drastically increase the performance of your LAMP setup. With the proper care and configuration, your caching solution will allow you to serve a greater number of users concurrently, and help ward off any possible DOS / Slashdot Effect you may encounter some day.
