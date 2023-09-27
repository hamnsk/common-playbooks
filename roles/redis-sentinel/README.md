redis
=========

Install and configure redis standalone or master-slave with or without sentinel.


Role Variables
--------------

	redis_use_sentinel: false
	
	redis_bind: "{{ansible_default_ipv4.address}}"
	redis_port: 6379
	
	redis_slaveof: # <masterip> <masterport>
	
	redis_slave_serve_stale_data: true
	redis_slave_read_only: true
	
	redis_protected_mode: false
	
	redis_timeout: 0
	redis_tcp_keepalive: 300
	
	redis_loglevel: notice
	redis_logfile: /var/log/redis/redis.log
	
	redis_databases: 16
	
	redis_save:
	  - 900 1
	  - 300 10
	  - 60 10000
	
	redis_activerehashing: true
	
	redis_sentinel_bind: "{{ansible_default_ipv4.address}}"
	redis_sentinel_port: 26379
	
	redis_sentinel_protected_mode: "{{redis_protected_mode}}"
	
	redis_sentinel_master_group_name: redis  # cluster name equivalent, same on all hosts
	
	redis_sentinel_logfile: /var/log/redis/sentinel.log
	
	redis_sentinel_down_after_milliseconds: 15000
	redis_sentinel_failover_timeout: 90000


Example Playbook
----------------

    - hosts: redis-servers
      roles:
         - { role: redis, redis_use_setinel: true, redis_slaveof: "10.0.0.150 6379" }


# Master
save ""
appendonly no
appendfsync no

# Slave 
save
appendonly yes
appendfsync everysec

sentinel notification-script mymaster /var/opt/rh/rh-redis32/redis/notify.sh