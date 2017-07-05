
PgBouncer
=========

PostgreSQL�����������ӳء�

��ҳ
    https://pgbouncer.github.io

Դ���룬bug׷��
    https://github.com/pgbouncer/pgbouncer

����
---------

PgBouncerȡ���ڼ��������ñ��룺

* `GNU Make`_ 3.81+
* libevent_ 2.0
* (��ѡ��) ����TLS֧�ֵ� OpenSSL_ 1.0.1��
* (��ѡ��) `c-ares`_ ��Ϊlibevent��evdns���滻��

.. _GNU Make: https://www.gnu.org/software/make/
.. _libevent: http://libevent.org/
.. _OpenSSL: https://www.openssl.org/
.. _`c-ares`: http://c-ares.haxx.se/

��װ�������Ժ�ֻ��Ҫ���� ::

    $ ./configure --prefix=/usr/local --with-libevent=libevent-prefix
    $ make
    $ make install

������Ǵ�git�����ģ�������Ϊ��Windows�����ģ���鿴����ֱ�Ĺ���˵����

DNS����֧��
------------------

��PgBouncer 1.4��ʼ����������ʱ���������ü���ʱִ�����������ҡ�
����Ҫ�ʵ����첽DNSʵ�֡������б���ʾ֧�ֵĺ�˺����ǵĲ鿴˳��

+----------------------------+----------+-----------+------------+----------------+---------------------------------------+
| ���                       | ����     | EDNS0 (1) | /etc/hosts | SOA ���� (2)   | ע��                                  |
+============================+==========+===========+============+================+=======================================+
| c-ares                     | yes      | yes       | yes        | yes            | ipv6+CNAME buggy in <=1.10            |
+----------------------------+----------+-----------+------------+----------------+---------------------------------------+
| udns                       | yes      | yes       | no         | yes            | ��ipv4                                |
+----------------------------+----------+-----------+------------+----------------+---------------------------------------+
| evdns, libevent 2.x        | yes      | no        | yes        | no             | ����� /etc/hosts ����                |
+----------------------------+----------+-----------+------------+----------------+---------------------------------------+
| getaddrinfo_a, glibc 2.9+  | yes      | yes (3)   | yes        | no             | N/A �ڷ�Linux��                       |
+----------------------------+----------+-----------+------------+----------------+---------------------------------------+
| getaddrinfo, libc          | no       | yes (3)   | yes        | no             | N/A ��win32�ϣ���Ҫpthreads           |
+----------------------------+----------+-----------+------------+----------------+---------------------------------------+
| evdns, libevent 1.x        | yes      | no        | no         | no             | buggy                                 |
+----------------------------+----------+-----------+------------+----------------+---------------------------------------+

1. EDNS0��Ҫ��һ�������������г���8����ַ��
2. ��Ҫ����SOA���������¼�������и��ĵ�������
3. Ҫ����EDNS0����� `options edns0` ��/etc/resolv.conf

`./configure` ���б�־ `--enable-evdns` �� `--disable-evdns`��
���ǹر��Զ�̽�Ⲣǿ��ʹ�� `evdns` �� `getaddrinfo_a()`��

��GIT����
-----------------

��GIT����PgBouncerҪ������ȡlibusual��ģ�鲢����ͷ�ļ��������ļ���Ȼ���������configure ::

	$ git clone https://github.com/pgbouncer/pgbouncer.git
	$ cd pgbouncer
	$ git submodule init
	$ git submodule update
	$ ./autogen.sh
	$ ./configure ...
	$ make
	$ make install

��Ҫ����İ���autoconf��automake��libtool��
autoconf-archive��python-docutils��pkg-config��

ΪWIN32����
------------------

Ŀǰֻ��env���Եİ汾��MINGW32 / MSYS��
Cygwin��Visual $ AnyYTHINGδ�����ԡ� DNS��������ѯ��ҪLibevent 2.x��

Ȼ��ִ��::

	$ ./configure ...
	$ make

�����Unix���н������::

	$ ./configure --host=i586-mingw32msvc ...

��WIN32������
----------------

�������������������ģ�����-d���ػ����̣���-R������������
��-u���л��û������ؽ���������

Ҫ��ΪWindows��������pgbouncer������Ҫ���� `service_name`
����Ϊ�����������֡�Ȼ��

	$ pgbouncer -regservice config.ini

Ҫж�ط���

	$ pgbouncer -unregservice config.ini

Ҫʹ��Windows�¼���־���������ļ�������"syslog = 1"��
����֮ǰ����Ҫע��pgbevent.dll::

	$ regsvr32 pgbevent.dll

Ҫж������ִ��::
    
        $ regsvr32 /u pgbevent.dll

