[![Latest Stable Version](https://poser.pugx.org/youzusg/etcd-php/v/stable)](https://packagist.org/packages/youzusg/etcd-php)
[![Total Downloads](https://poser.pugx.org/youzusg/etcd-php/downloads)](https://packagist.org/packages/youzusg/etcd-php)
[![Latest Unstable Version](https://poser.pugx.org/youzusg/etcd-php/v/unstable)](https://packagist.org/packages/youzusg/etcd-php)
[![License](https://poser.pugx.org/youzusg/etcd-php/license)](https://packagist.org/packages/youzusg/etcd-php)

# Etcd client library for PHP

etcd is a distributed configuration system, part of the coreos project.

This repository provides a client library for etcd for PHP applications.

## Installing and running etcd

```bash
git clone https://github.com/coreos/etcd.git
cd etcd
./build
./bin/etcd
````


## Usage

### The client

```php
    // $client = new Client($server); 
    $client = new Client($server, $username, $password);
    $client->set('/foo', 'fooValue');
    // Set the ttl
    $client->set('/foo', 'fooValue', 10);
    // get key value
    echo $client->get('/foo');
    
    // Update value with key
    $client->update('/foo', 'newFooValue');
    
    // Delete key
    $client->rm('/foo');

    // Create a directory
    $client->mkdir('/fooDir');
    // Remove dir
    $client->rmdir('/fooDir');
    
```

### The command line tool

#### Setting Key Values

Set a value on the `/foo/bar` key:

```bash
$ bin/etcd-php etcd:set /foo/bar "Hello world"
```

Set a value on the `/foo/bar` key with a value that expires in 60 seconds:

```bash
$ bin/etcd-php etcd:set /foo/bar "Hello world" --ttl=60
```

Create a new key `/foo/bar`, only if the key did not previously exist:

```bash
$ bin/etcd-php etcd:mk /foo/new_bar "Hello world"
```

Create a new dir `/fooDir`, only if the key did not previously exist:

```bash
$ bin/etcd-php etcd:mkdir /fooDir
```

Update an existing key `/foo/bar`, only if the key already existed:

```bash
$ bin/etcd-php etcd:update /foo/bar "Hola mundo"
```

Create or update a directory called `/mydir`:

```bash
$ bin/etcd-php etcd:setDir /mydir
```


#### Retrieving a key value

Get the current value for a single key in the local etcd node:

```bash
$ bin/etcd-php etcd:get /foo/bar
```

#### Listing a directory

Explore the keyspace using the `ls` command

```bash
$ bin/etcd-php etcd:ls
/akey
/adir
$ bin/etcd-php etcd:ls /adir
/adir/key1
/adir/key2
```

Add `-recursive` to recursively list subdirectories encountered.

```bash
$ bin/etcd-php etcd:ls --recursive
/foo
/foo/bar
/foo/new_bar
/fooDir
```


### Deleting a key

Delete a key:

```bash
$ bin/etcd-php etcd:rm /foo/bar
```

Delete an empty directory or a key-value pair

```bash
$ bin/etcd-php etcd:rmdir /path/to/dir 
```

Recursively delete a key and all child keys:

```bash
$ bin/etcd-php etcd:rmdir /path/to/dir --recursive
```

#### Watching for changes

Watch for only the next change on a key:

```bash
$ bin/etcd-php etcd:watch /foo/bar
```
