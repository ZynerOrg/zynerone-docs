Open `data/conf/postfix/extra.cf` and set the `message_size_limit` accordingly in bytes. See `main.cf` for the default value.

You will also need to adjust message size in Rspamd and Clamav configurations:

+ in `data/conf/rspamd/local.d/options.inc` add `max_message` parameter, check [Rspamd Docs](https://rspamd.com/doc/configuration/options.html#:~:text=DoS%20(default%3A%201024)-,max_message,-maximum%20size%20of) for defaults
+ in `data/conf/rspamd/local.d/external_services.conf` adjust `max_size` parameter for `oletools`
+ in `data/conf/rspamd/local.d/antivirus.conf` adjust `max_size` parameter for `clamav`
+ in `data/conf/clamav/clamd.conf` adjust `MaxScanSize` and `MaxFileSize`


Restart Postfix, Rspamd and Clamav:
=== "docker compose (Plugin)"

    ``` bash
    docker compose restart postfix-mailcow rspamd-mailcow clamd-mailcow
    ```

=== "docker-compose (Standalone)"

    ``` bash
    docker-compose restart postfix-mailcow rspamd-mailcow clamd-mailcow
    ```
