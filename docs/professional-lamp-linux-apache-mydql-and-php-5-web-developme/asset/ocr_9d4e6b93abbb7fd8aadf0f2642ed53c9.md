# Caching Engines

| Directive | Default | Set In | Description |
| :--- | :--- | :--- | :--- |
| `eaccelerator_shm_max` | `0` (no limit) | `php.ini` and `httpd.conf` | Specifies the maximum size for data put into shared memory using the `eaccelerator_put()` PHP function. Numeric values are specified in bytes, and a value of 0 disables the limit. |
| `eaccelerator_shm_ttl` | `0` (never remove stale scripts) | `php.ini` and `httpd.conf` | Defines how many seconds a script will stay cached by `eAccelerator` in shared memory before it is allowed to be removed from the cache in favor of new requests. A value of 0 indicates that items should never be removed, and could cause the shared memory cache to eventually fill and prevent new requests from being cached. |
| `eaccelerator_shm_prune_period` | `0` (never remove stale items) | `php.ini` and `httpd.conf` | Similar to the `shm_ttl` setting, this directive controls the collection of stale scripts from the shared memory cache. Instead of acting as a timeout for individual scripts in the cache, `shm_prune_period` works by removing stale items only if the value defined in `shm_prune_period` has elapsed. This value is expressed in number of seconds, and a value of 0 tells `eAccelerator` not to try to remove stale items. |
| `eaccelerator_shm_only` | `0` (use both) | `php.ini` and `httpd.conf` | Enables and disables (0 or 1) the on-disk cache. A value of 0 tells `eAccelerator` to use both a shared memory and file-based disk cache, whereas a value of 1 tells `eAccelerator` to use shared memory only. |
| `eaccelerator_compress` | `1` (enable compression) | `php.ini`, `httpd.conf`, `.htaccess`, and user scripts | This directive enables and disables output content compression, similar to Apache's `mod_deflate` or PHP's `gzip` output buffering. |
| `eaccelerator_compress_level` | `9` (maximum compression) | `php.ini`, `httpd.conf`, `.htaccess`, and user scripts | This setting controls the level of compression used when using the output compression enabled in `eaccelerator_compress`. The maximum value of 9 uses high compression, resulting in smaller transferred file sizes, while lower values decrease compression and increase transferred size. |

*Table continued on following page*

293