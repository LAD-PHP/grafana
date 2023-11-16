auth_enabled: false

server:
  http_listen_port: 3100

common:
  path_prefix: /loki
  storage:
    filesystem:
      chunks_directory: /loki/chunks
      rules_directory: /loki/rules
  replication_factor: 1
  ring:
    kvstore:
      store: inmemory

schema_config:
  configs:
    - from: 2020-10-24
      store: boltdb-shipper
      object_store: filesystem
      schema: v11
      index:
        prefix: index_
        period: 24h
storage_config:
  aws:
    s3: "s3://on-u4-loki-logs"
    bucketname: "on-u4-loki-logs"
    #region: "your_region"
    endpoint: "s3console.oncloud.ru" # Если используется другой endpoint, укажите соответствующий
    access_key_id: "on-u4"
    secret_access_key: "uc5EeMii0xah"
    insecure: false
    s3ForcePathStyle: true
compactor:
  retention_delete_delay: 2h
  retention_delete_worker_count: 150
  retention_enabled: true
  working_directory: /loki/compactor
  shared_store: s3
  compaction_interval: 1h

ruler:
  alertmanager_url: http://localhost:9093

# By default, Loki will send anonymous, but uniquely-identifiable usage and configuration
# analytics to Grafana Labs. These statistics are sent to https://stats.grafana.org/
#
# Statistics help us better understand how Loki is used, and they show us performance
# levels for most users. This helps us prioritize features and documentation.
# For more information on what's sent, look at
# https://github.com/grafana/loki/blob/main/pkg/usagestats/stats.go
# Refer to the buildReport method to see what goes into a report.
#
# If you would like to disable reporting, uncomment the following lines:
#analytics:
#  reporting_enabled: false