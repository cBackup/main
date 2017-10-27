!!! note "Description"
    API v2 is RESTful API for exporting data to embed it to the external services.

# Available methods

* **List nodes**

        /index.php?r=v2/node/search
        /index.php?r=v2/node/search&limit=1
        /index.php?r=v2/node/search&offset=1
        /index.php?r=v2/node/search&limit=1&offset=1

* **Retrieve one node**
  
        /index.php?r=v2/node/get&id=1

# Examples

**1. Search nodes by 'IN' or 'LIKE' criteria joined via 'AND' operand**

```php
$ch = curl_init();
      curl_setopt_array($ch, [
          CURLOPT_URL        => 'http://SITE_NAME/index.php?r=v2/node/search',
          CURLOPT_HEADER     => false,
          CURLOPT_POST       => 1,
          CURLOPT_HTTPHEADER => [
              "Accept: application/json",
              "Cache-Control: no-cache",
              "Authorization: Bearer CHICKEN-CHICKEN-CHICKEN-CHICKEN-CHICKEN" 
          ],
          CURLOPT_POSTFIELDS => [
              'mac' => json_encode(['001122334455', '001122334456']), // will be treated as 'IN'
              'ip'  => json_encode('172.16.22'),                      // will be treated as 'LIKE %%'
          ]
      ]);
      curl_exec($ch);
      curl_close($ch);
```

* All post fields array keys (parameter names for `CURLOPT_POSTFIELDS`) must be valid `Node` model attributes.
* All post fields array values must be after `json_encode()`
* The code above will produce the following query:

        SELECT * FROM node 
          WHERE (
            mac IN ('001122334455', '001122334456')
          ) 
          AND (ip LIKE '%172.16.22%')

---------

**2. Lookup nodes by 'LIKE %%' non-strict match joined via 'OR' operand**

```php
$ch = curl_init();
      curl_setopt_array($ch, [
          CURLOPT_URL        => 'http://backup.local/index.php?r=v2/node/lookup',
          CURLOPT_HEADER     => false,
          CURLOPT_POST       => 1,
          CURLOPT_HTTPHEADER => [
              "Accept: application/json",
              "Cache-Control: no-cache",
              "Authorization: Bearer CHICKEN-CHICKEN-CHICKEN-CHICKEN-CHICKEN" 
          ],
          CURLOPT_POSTFIELDS => [
              'mac' => json_encode(['001122334455', '001122334456']),
              'ip'  => json_encode('172.16.22'),
          ]
      ]);
      curl_exec($ch);
      curl_close($ch);
```

The code above will produce the following query:

```sql
SELECT * FROM `node` 
  WHERE (
    (`mac` LIKE '%001122334455%') OR (`mac` LIKE '%001122334456%')
  ) 
  OR (`ip` LIKE '%172.16.22%')
```
