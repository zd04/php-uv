# php-uv

[![Build Status](https://secure.travis-ci.org/chobie/php-uv.png)](http://travis-ci.org/chobie/php-uv)

interface to libuv for php (experimental). also supports http-parser.

# Experimental

This extension is experimental, its functions may change their names 
or move to extension all together so do not rely to much on them you have been warned!

# Install

````
git clone https://github.com/chobie/php-uv.git --recursive
cd php-uv
(cd libuv && make)
phpize
./configure
make
make install
# add `extension=uv.so` to your php.ini
````

# Examples

see examples and tests directory.

````
<?php
$tcp = uv_tcp_init();

uv_tcp_bind($tcp, uv_ip4_addr('0.0.0.0',8888));

uv_listen($tcp,100, function($server){
    $client = uv_tcp_init();
    uv_accept($server, $client);
    var_dump(uv_tcp_getsockname($server));

    uv_read_start($client, function($socket, $nread, $buffer){
        var_dump($buffer);
        uv_close($socket);
    });
});

$c = uv_tcp_init();
uv_tcp_connect($c, uv_ip4_addr('0.0.0.0',8888), function($stream, $stat){
    if ($stat == 0) {
        uv_write($stream,"Hello",function($stream, $stat){
            uv_close($stream);
        });
    }
});

uv_run();
````

# Community

Check out #php-uv on irc.freenode.net.

# Author

* Shuhei Tanuma

# License

PHP License


# Documents

## void uv_unref(resource $uv_t)


## long uv_last_error([resource $uv_loop])


## string uv_err_name(long $error_code)


## string uv_strerror(long $error_code)


## void uv_update_time(resource $uv_loop)


## void uv_ref(resource $uv_handle)


## void uv_run([resource $uv_loop])


## void uv_run_once([resource $uv_loop])


## void uv_loop_delete(resource $uv_loop)


## long uv_now(resource $uv_loop)


## void uv_tcp_bind(resource $uv_sockaddr)


## void uv_tcp_bind6(resource $uv_sockaddr)


## void uv_write(resource $handle, string $data, callable $callback)


## void uv_write(resource $handle, string $data, callable $callback)


## void uv_tcp_nodelay(resource $handle, bool $flag)


## void uv_accept(resource $server, resource $client)


## void uv_shutdown(resource $handle, callable $callback)


## void uv_close(resource $handle, callable $callback)


## void uv_read_start(resource $handle, callable $callback)


## void uv_read2_start(resource $handle, callable $callback)


## void uv_read_stop(resource $handle)


## resource uv_ip4_addr(string $ipv4_addr, long $port)


## resource uv_ip6_addr(string $ipv6_addr, long $port)


## void uv_listen(resource $handle, long $backlog, callable $callback)


## void uv_tcp_connect(resource $handle, string $ipv4_addr, callable $callback)


## void uv_tcp_connect6(resource $handle, string $ipv6_addr, callable $callback)


## resource uv_timer_init([resource $loop])


## void uv_timer_start(resource $timer, long $timeout, long $repeat, callable $callback)


## void uv_timer_stop(resource $timer)


## void uv_timer_again(resource $timer)


## void uv_timer_set_repeat(resource $timer, long $repeat)


## long uv_timer_get_repeat(resource $timer)


## void uv_idle_start(resource $idle, callable $callback)


## void uv_getaddrinfo(resource $loop, callable $callback, string $node, string $service, array $hints)


## void uv_idle_stop(resource $idle)


## resource uv_tcp_init([resource $loop])


## resource uv_idle_init([resource $loop])


## resource uv_default_loop()


## resource uv_loop_new()


## resource uv_udp_init([resource $loop])


## void uv_udp_bind(resource $resource, resource $address, long $flags)


## void uv_udp_bind6(resource $resource, resource $address, long $flags)


## void uv_udp_recv_start(resource $handle, callable $callback)


## void uv_udp_recv_stop(resource $handle)


## long uv_udp_set_membership(resource $handle, string $multicast_addr, string $interface_addr, long $membership)


## void uv_udp_set_multicast_loop(resource $handle, long $enabled)


## void uv_udp_set_multicast_ttl(resource $handle, long $ttl)


## void uv_udp_set_broadcast(resource $handle, bool $enabled)


## void uv_udp_send(resource $handle, string $data, resource $uv_addr, callable $callback)


## void uv_udp_send6(resource $handle, string $data, resource $uv_addr6, callable $callback)


## bool uv_is_active(resource $handle)


## bool uv_is_readable(resource $handle)


## bool uv_is_writable(resource $handle)


## bool uv_walk(resource $loop, callable $closure[, array $opaque])


## resource uv_pipe_init(resource $loop, long $ipc)


## void uv_pipe_open(resource $handle, long $pipe)


## long uv_pipe_bind(resource $handle, string $name)


## void uv_pipe_connect(resource $handle, string $path, callable $callback)


## void uv_pipe_pending_instances(resource $handle, long $count)


## resource uv_ares_init_options(resource $loop, array $options, long $optmask)


## void ares_gethostbyname(resource $handle, string $name, long $flag, callable $callback)


## array uv_loadavg(void)


## double uv_uptime(void)


## long uv_get_free_memory(void)


## long uv_get_total_memory(void)


## long uv_hrtime(void)


## string uv_exepath(void)


## string uv_cwd(void) 

## array uv_cpu_info(void)


## array uv_interface_addresses(void)


## resource uv_spawn(resource $loop, string $command, array $args, array $context, callable $callback)


## void uv_process_kill(resource $handle, long $signal)
TODO: 

## void uv_kill(long $pid, long $signal)


## bool uv_chdir(string $directory)


## resource uv_rwlock_init(void)


## uv_rwlock_rdlock(resource $handle)


## bool uv_rwlock_tryrdlock(resource $handle)


## void uv_rwlock_rdunlock(resource $handle)


## uv_rwlock_wrlock(resource $handle)


## uv_rwlock_trywrlock(resource $handle)


## uv_rwlock_wrunlock(resource $handle)


## uv_lock uv_mutex_init(void) 

## void uv_mutex_lock(uv_lock $lock)

## bool uv_mutex_trylock(uv_lock $lock) 

## uv_lock uv_sem_init(void)


## void uv_sem_post(uv_lock $sem)


## void uv_sem_wait(uv_lock $sem)


## void uv_sem_trywait(uv_lock $sem)


## resource uv_prepare_init(resource $loop)


## void uv_prepare_start(resource $handle, callable $callback)


## void uv_prepare_stop(resource $handle)


## resoruce uv_check_init([resource $loop])


## void uv_check_start(resource $handle, callable $callback)


## void uv_check_stop(resource $handle)


## resource uv_async_init(resource $loop, callable $callback)


## void uv_async_send(resource $handle)


## void uv_queue_work(resource $loop, callable $callback, callable $after_callback)


## resource uv_fs_open(resource $loop, string $path, long $flag, long $mode, callable $callback)


## void uv_fs_read(resoruce $loop, zval $fd, callable $callback)


## void uv_fs_close(resource $loop, zval $fd, callable $callback)


## void uv_fs_write(resource $loop, zval $fd, string $buffer, long $offset, callable $callback)


## void uv_fs_fsync(resource $loop, zval $fd, callable $callback)


## void uv_fs_fdatasync(resource $loop, zval $fd, callable $callback)


## void uv_fs_ftruncate(resource $loop, zval $fd, long $offset, callable $callback)


## void uv_fs_mkdir(resource $loop, string $path, long $mode, callable $callback)


## void uv_fs_rmdir(resource $loop, string $path, callable $callback)


## void uv_fs_unlink(resource $loop, string $path, callable $callback)


## void uv_fs_rename(resource $loop, string $from, string $to, callable $callback)


## void uv_fs_utime(resource $loop, string $path, long $utime, long $atime, callable $callback)


## void uv_fs_futime(resource $loop, zval $fd, long $utime, long $atime callable $callback)


## void uv_fs_chmod(resource $loop, string $path, long $mode, callable $callback)


## void uv_fs_fchmod(resource $loop, zval $fd, long $mode, callable $callback)


## void uv_fs_chown(resource $loop, string $path, long $uid, long $gid, callable $callback)


## void uv_fs_fchown(resource $loop, zval $fd, long $uid, $long $gid, callable $callback)


## void uv_fs_link(resource $loop, string $from, string $to, callable $callback)


## void uv_fs_symlink(resource $loop, string $from, string $to, long $flags, callable $callback)


## void uv_fs_readlink(resource $loop, string $path, callable $callback)


## void uv_fs_stat(resource $loop, string $path, callable $callback)


## void uv_fs_lstat(resource $loop, string $path, callable $callback)


## void uv_fs_fstat(resource $loop, zval $fd, callable $callback)


## uv_fs_readdir(resource $loop, string $path, long $flags, callable $callback)


## void uv_fs_sendfile(resource $loop, zval $in_fd, zval $out_fd, long $offset, long $length, callable $callback)


## resource uv_fs_event_init(resource $loop, string $path, callable $callback, long $flags = 0)


## resource uv_tty_init(resource $loop, zval $fd, long $readable)


## long uv_tty_get_winsize(resource $tty, long &$width, long &$height)


## long uv_tty_set_mode(resource $tty, long $mode)


## void uv_tty_reset_mode(void)


## string uv_tcp_getsockname(resource $uv_sockaddr)


## string uv_tcp_getpeername(resource $uv_sockaddr)


## string uv_udp_getsockname(resource $uv_sockaddr)


## long uv_resident_set_memory(void)


## string uv_ip4_name(resource uv_sockaddr $address)


## string uv_ip6_name(resource uv_sockaddr $address)


## uv uv_poll_init([resource $uv_loop], zval fd)


## uv uv_poll_start(resource $handle, $events, $callback)


## void uv_poll_stop(resource $poll)


## uv uv_fs_poll_init([resource $uv_loop])


## uv uv_fs_poll_start(resource $handle, $callback, string $path, long $interval)


## void uv_fs_poll_stop(resource $poll)


## resource uv_http_parser_init(long $target = UV::HTTP_REQUEST)


## bool uv_http_parser_execute(resource $parser, string $body, array &$result)


