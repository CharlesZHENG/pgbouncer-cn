
pgbouncer
#########

��Ҫ
========

::

  pgbouncer [-d][-R][-v][-u user] <pgbouncer.ini>
  pgbouncer -V|-h

��Windows������ϣ�ѡ����:

  pgbouncer.exe [-v][-u user] <pgbouncer.ini>
  pgbouncer.exe -V|-h

����Windows���������ѡ��::

  pgbouncer.exe --regservice   <pgbouncer.ini>
  pgbouncer.exe --unregservice <pgbouncer.ini>

����
===========

**pgbouncer**��һ��PostgreSQL���ӳء�
�κ�Ŀ��Ӧ�ó��򶼿������ӵ�**pgbouncer**��
��������PostgreSQL������һ����**pgbouncer**��������ʵ�ʷ����������ӣ�
����������������һ�����е����ӡ�

**pgbouncer**��Ŀ����Ϊ�˽��ʹ�PostgreSQL������ʱ������Ӱ�졣

Ϊ�˲�Ӱ�����ӳص��������壬**pgbouncer**���л�����ʱ֧�ֶ������͵ĳأ�

�Ự���ӳ�
    ����ò�ķ��������ͻ�������ʱ�����ڿͻ��˱������ӵ���������ʱ���ڷ���һ�����������ӡ�
    ���ͻ��˶Ͽ�����ʱ�����������ӽ��Żص����ӳ��С�����Ĭ�ϵķ�����

�������ӳ�
    ����������ֻ����һ���������ʱ��Ÿ���ͻ��ˡ�
    ��PgBouncerע�⵽���������ʱ�򣬷��������ӽ���Ż����ӳ��С�

������ӳ�
    �����ģʽ���ڲ�ѯ��ɺ󣬷��������ӽ��������Ż����ӳ��С�
    ���ģʽ�в����������������Ϊ���ǻ��жϡ�

**pgbouncer**�Ĺ�����������ӵ����⡮���⡯���ݿ�**pgbouncer**ʱ���õ�һЩ�µ�
``SHOW``������ɡ�

���ٿ�ʼ
===========

�������ú��÷����¡�

1. ����һ��pgbouncer.ini�ļ���**pgbouncer(5)**����ϸ��Ϣ��������::

    [databases]
    template1 = host=127.0.0.1 port=5432 dbname=template1
    
    [pgbouncer]
    listen_port = 6543
    listen_addr = 127.0.0.1
    auth_type = md5
    auth_file = users.txt
    logfile = pgbouncer.log
    pidfile = pgbouncer.pid
    admin_users = someuser

2. ���������û�׼���``users.txt``�ļ�::

    "someuser" "same_password_as_in_server"

3. ����**pgbouncer**::

     $ pgbouncer -d pgbouncer.ini

4. ���Ӧ�ó��򣨻�**�ͻ���psql**���Ѿ����ӵ�**pgbouncer**
������ֱ�����ӵ�PostgreSQL����������

    $ psql -p 6543 -U someuser template1

5. ͨ�����ӵ��������Ա���ݿ�**pgbouncer**����**pgbouncer**��
����``show help;``��ʼ��

      $ psql -p 6543 -U someuser pgbouncer
      pgbouncer=# show help;
      NOTICE:  Console usage
      DETAIL:
        SHOW [HELP|CONFIG|DATABASES|FDS|POOLS|CLIENTS|SERVERS|SOCKETS|LISTS|VERSION]
        SET key = arg
        RELOAD
        PAUSE
        SUSPEND
        RESUME
        SHUTDOWN

6. ������޸���pgbouncer.ini�ļ��������������������¼��أ�

      pgbouncer=# RELOAD;

�����п���
=====================

-d
    �ں�̨���С�û���������̽���ǰ̨���С�
    ע�⣺��Windows�ϲ������ã�**pgbouncer**��Ҫ��Ϊ�������С�

-R
    ������������������ζ�����ӵ��������еĽ��̣����м��ش򿪵��׽��֣�
    Ȼ��ʹ�����ǡ����û�л���̣�������������
    ע�⣺ֻ���ڲ���ϵͳ֧��Unix�׽����ҡ�unix_socket_dir��
    ��������δ������ʱ�ſ��á���Windows�����ϲ������á�
    ��ʹ��TLS���ӣ����Ǳ�ɾ���ˡ�

-u user
    ����ʱ�л����������û���

-v
    ������ϸ�ȡ��ɶ��ʹ�á�

-q
    ���� - ��Ҫ�ǳ���stdout����ע�⣬
    �ⲻӰ����־��ϸ�̶ȣ�ֻ�и�stdout����ʹ�á�����init.d�ű���

-V
    ��ʾ�汾��

-h
    ��ʾ��̵İ�����

--regservice
    Win32��ע��pgbouncer��ΪWindows�������С� **service_name**
    ���ò���ֵ����Ҫע������ơ�

--unregservice
    Win32: ע��Windows����

�������̨
=============

ͨ���������ӵ����ݿ�**pgbouncer**����ʹ�ÿ���̨::

  $ psql -p 6543 pgbouncer

ֻ�������ò���**admin_users**��**stats_users**���г����û��������¼������̨��
������`auth_mode=any`ʱ���κ��û���������Ϊstats_user��¼����

���⣬���ͨ��Unix�׽��ֵ�¼�����ҿͻ��˾��������н�����ͬ��Unix�û�uid��
�����û���**pgbouncer**��ʹ�������¼��

��ʾ����
~~~~~~~~~~~~~

**SHOW**���������Ϣ������������ÿ�����

SHOW STATS;
-----------

��ʾͳ����Ϣ��

database
    Ϊÿ�����ݿ��ṩͳ����Ϣ��

total_requests
    ��**pgbouncer**���ܵ�SQL����������

total_received
    **pgbouncer**�յ��������������ֽ�����

total_sent
    **pgbouncer**���͵������������ֽ�����

total_query_time
    ���������ӵ�PostgreSQLʱ**pgbouncer**���ѵ�΢������

avg_req
    �ϴ�ͳ���ڼ�ÿ��ƽ����������

avg_recv
    ÿ��ƽ�����գ��ӿͻ��ˣ��ֽڡ�

avg_sent
    ÿ��ƽ�����ͣ����ͻ��ˣ��ֽڡ�

avg_query
    ƽ����ѯ����ʱ�䣨��΢��Ϊ��λ����

SHOW SERVERS;
-------------

type
    S�����ڷ�������

user
    **pgbouncer**�������ӵ����������û����� 

database
    ���ݿ�����

state
    pgbouncer���������ӵ�״̬��**active**��**used**��
    **idle**֮һ��

addr
  PostgreSQL server��������IP��ַ��

port
    PostgreSQL�������Ķ˿ڡ�

local_addr
    �������������ĵ�ַ��

local_port
    �����ϵ����������˿ڡ�

connect_time
    �������ӵ�ʱ�䡣

request_time
    ���һ�����󷢳���ʱ�䡣

ptr
    �����ӵ��ڲ�����ĵ�ַ������ΨһID��

link
    ��������ԵĿͻ������ӵ�ַ��

remote_pid
    ��˷��������̵�pid�����ͨ��unix�׽��ֽ������ӣ�
    ����OS֧�ֻ�ȡ����ID��Ϣ����ΪOS pid��
    ���������ӷ��������͵�ȡ�����ݰ�����ȡ�����������������Postgres��
    ��Ӧ����PID�������������������һ��PgBouncer��������һ���������

SHOW CLIENTS;
-------------

type
    C�����ڿͻ��ˡ�

user
    �ͻ��������û���

database
    ���ݿ����ơ�

state
    �ͻ������ӵ�״̬��**active**��**used**��**waiting**
    ��**idle**֮һ��

addr
    �ͻ��˵�IP��ַ��

port
    �ͻ������ӵ��Ķ˿ڡ�

local_addr
    �����ϵ����ӽ�����ַ��

local_port
    �����ϵ����ӽ����˿ڡ�

connect_time
    ����ʱ��ʱ�����

request_time
    ���һ�οͻ��������ʱ�����

ptr
    �����ӵ��ڲ�����ĵ�ַ������ΨһID��

link
    �ͻ�����Եķ��������ӵ�ַ��

remote_pid
    ����ID���ڿͻ���ͨ��UNIX�׽������Ӳ���OS֧�ֻ�ȡ��������¡�

SHOW POOLS;
-----------

Ϊÿ��(database, user)����һ���µ����ӳ�ѡ�

database
    ���ݿ����ơ�

user
    �û�����

cl_active
    ���ӵ����������Ӳ����Դ����ѯ�Ŀͻ������ӡ�

cl_waiting
    �ѷ��Ͳ�ѯ����δ��÷��������ӵĿͻ������ӡ�

sv_active
    ���ӵ��ͻ��˵ķ��������ӡ�

sv_idle
    δʹ���ҿ��������ڿͻ�����ѯ�ķ��������ӡ�

sv_used
    �Ѿ����ó���`server_check_delay`ʱ���ķ��������ӣ�
    ������������ʹ��֮ǰ����Ҫ����`server_check_query`��

sv_tested
    ��ǰ��������`server_reset_query`��`server_check_query`�ķ��������ӡ�

sv_login
    ��ǰ���ڵ�¼�����еķ��������ӡ�

maxwait
    �����е�һ�������ϵģ��ͻ����Ѿ��ȴ��˶೤ʱ�䣬����ơ�
    �������ʼ���ӣ���ô��������ǰ�����ӳش���������ٶȲ����졣
    ԭ������Ƿ��������ع��ػ�**pool_size**���ù�С��

pool_mode
    ����ʹ�õ����ӳ�ģʽ��

SHOW LISTS;
-----------

���У������У�����ʾ�����ڲ���Ϣ��

databases
    ���ݿ������

users
    �û�������

pools
    ���ӳؼ�����

free_clients
    ���пͻ��˼�����

used_clients
    ʹ���˵Ŀͻ��˼�����

login_clients
    ��**login**״̬�еĿͻ��˼�����

free_servers
    ���з�����������

used_servers
    ʹ���˵ķ�����������

SHOW USERS;
-----------

name
    �û���

pool_mode
    �û���д��pool_mode�����ʹ��Ĭ��ֵ���򷵻�NULL��

SHOW DATABASES;
---------------

name
    ���õ����ݿ�������ơ�

host
    pgbouncer���ӵ���������

port
    pgbouncer���ӵ��Ķ˿ڡ�

database
    pgbouncer���ӵ���ʵ�����ݿ����ơ�

force_user
    ���û��������ַ�����һ����ʱ��pgbouncer��PostgreSQL
    ֮������ӱ�ǿ�Ƹ��������û������ܿͻ����û���˭��

pool_size
    ���������ӵ����������

pool_mode
    ���ݿ����дpool_mode�����ʹ��Ĭ��ֵ�򷵻�NULL��

SHOW FDS;
---------

�ڲ����� - ��ʾ�븽�����ڲ�״̬һ��ʹ�õ�fds�б�

�����ӵ��û�ʹ���û���"pgbouncer"ʱ��
ͨ��Unix�׽������Ӳ����������й�����ͬ��UID��ʵ�ʵ�fdsͨ�����Ӵ��ݡ�
�û������ڽ�������������
ע�⣺�ⲻ������Windows������

���������ֹ�ڲ��¼�ѭ���������ʹ��PgBouncerʱ��Ӧ��ʹ������

fd
    �ļ���������ֵ��

task
    **pooler**��**client**��**server**֮һ��

user
    ʹ�ø�FD�����ӵ��û���

database
    ʹ�ø�FD�����ӵ����ݿ⡣

addr
    ʹ��FD�����ӵ�IP��ַ�����ʹ��unix�׽�������**unix**��

port
    ʹ��FD�����ӵĶ˿ڡ�

cancel
    ȡ�������ӵļ���

link
    ��Ӧ������/�ͻ��˵�fd�����������ΪNULL��

SHOW CONFIG;
------------

��ʾ��ǰ���������ã�һ��һ�������������ֶΣ�

key
    ���ñ�����

value
    ����ֵ

changeable
    **yes**����**no**����ʾ����ʱ�����Ƿ�ɸ��ġ�
    �����**no**����ñ���ֻ��������ʱ�ı䡣

SHOW DNS_HOSTS;
---------------

��ʾDNS�����е���������

hostname
    ��������

ttl
    ֱ����һ�β��Ҿ����˶����롣

addrs
    ��ַ�Ķ��ŷָ����б�

SHOW DNS_ZONES
--------------

��ʾ�����е�DNS����

zonename
    �������ơ�

serial
    ��ǰ���кš�

count
    
    ���ڴ��������������


���̿�������
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PAUSE [db];
-----------

PgBouncer���ԶϿ����з����������ӣ����ȵȴ����в�ѯ��ɡ�
���в�ѯ���֮ǰ������᷵�ء������ݿ���������ʱʹ�á�

����ṩ�����ݿ����ƣ���ôֻ�и����ݿ⽫����ͣ��

DISABLE db;
-----------

�ܾ��������ݿ��ϵ������¿ͻ������ӡ�

ENABLE db;
----------

����һ����**DISABLE**����֮�������µĿͻ������ӡ�

KILL db;
--------

����ɾ���������ݿ��ϵ����пͻ��˺ͷ��������ӡ�

SUSPEND;
--------

�����׽��ֻ�������ˢ�£�PgBouncerֹͣ���������ϵ����ݡ�
�����л�����Ϊ��֮ǰ������᷵�ء���PgBouncer������������ʱʹ�á�

RESUME [db];
------------

��֮ǰ��**PAUSE**��**SUSPEND**�����лָ�������

SHUTDOWN;
---------

PgBouncer���̽����˳���

RELOAD;
-------

PgBouncer���̽����¼������������ļ������¿ɸı�����á�

�ź�
~~~~~~~

SIGHUP
    ���¼������á����ڿ���̨�Ϸ�������**RELOAD;**��ͬ��

SIGINT
    ��ȫ�رա����ڿ���̨�Ϸ���**PAUSE;**��**SHUTDOWN;**��ͬ��

SIGTERM
    �����رա����ڿ���̨�Ϸ���**SHUTDOWN;**��ͬ��

Libevent����
~~~~~~~~~~~~~~~~~

����libevent���ĵ�::

  ����ͨ���ֱ����û�������EVENT_NOEPOLL��EVENT_NOKQUEUE��
  VENT_NODEVPOLL��EVENT_NOPOLL��EVENT_NOSELECT�����ö�
  epoll��kqueue��devpoll��poll��select��֧�֡�

  ͨ�����û�������EVENT_SHOW_METHOD��libevent��ʾ��ʹ�õ��ں�֪ͨ������

�ּ�
========

pgbouncer(5) - ���������������ֲ�ҳ

https://pgbouncer.github.io/

https://wiki.postgresql.org/wiki/PgBouncer

