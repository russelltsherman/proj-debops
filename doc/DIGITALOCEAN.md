# DIGITALOCEAN

see [Digital Ocean API documentation](https://developers.digitalocean.com/documentation/v2/) for more details.

## API

use these curl commands to query the Digital Ocean API to see what options are available.

### Export your API Token

```bash
export TF_VAR_do_api_token='<digital-ocean-api-token>'
```

### list available Images

request a list of images

```bash
curl -X GET\
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TF_VAR_do_api_token" \
  "https://api.digitalocean.com/v2/images?page=1&per_page=1000"
```

response includes images, details, and regions available

```json
{
  "images":[
    {
      "id":24438994,
      "name":"1381.1.0 (beta)",
      "distribution":"CoreOS",
      "slug":"coreos-beta",
      "public":true,
      "regions":["nyc1","sfo1","nyc2","ams2","sgp1","lon1","nyc3","ams3","fra1","tor1","sfo2","blr1"],
      "created_at":"2017-04-26T19:26:27Z",
      "min_disk_size":20,
      "type":"snapshot",
      "size_gigabytes":0.33
    }
  ],
  "links":{},
  "meta":{"total":1}
}
```

### List available Regions

request a list of regions

```bash
curl -X GET \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TF_VAR_do_api_token" \
  "https://api.digitalocean.com/v2/regions"
```

response includes sizes and features available in each region

```json
{
  "regions":[
    {
      "name":"New York 1",
      "slug":"nyc1",
      "sizes":["512mb","1gb","2gb","4gb","8gb"],
      "features":["private_networking","backups","ipv6","metadata","install_agent","storage"],
      "available":true
    }
  ],
  "links":{},
  "meta":{"total":1}
}
```

### List available Sizes

request a list of sizes

```bash
curl -X GET \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TF_VAR_do_api_token" \
  "https://api.digitalocean.com/v2/sizes"
```

response includes sizes, details, and regions available

```json
{
  "sizes":[
    {
      "slug":"512mb",
      "memory":512,
      "vcpus":1,
      "disk":20,
      "transfer":1.0,
      "price_monthly":5.0,
      "price_hourly":0.00744,
      "regions":["ams2","ams3","blr1","fra1","lon1","nyc1","nyc2","nyc3","sfo1","sfo2","sgp1","tor1"],
      "available":true
    }
  ],
  "links":{},
  "meta":{"total":1}
}
```


### Create SSH Key

read local id_rsa.pub key and create a key on digital ocean

```bash
SSH_KEY=$(<~/.ssh/id_rsa.pub)
SSH_KEY_NAME=$(echo $SSH_KEY | cut -d' ' -f3)

curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TF_VAR_do_api_token" \
  -d "{\"name\":\"$SSH_KEY_NAME\",\"public_key\":\"$SSH_KEY\"}" \
  "https://api.digitalocean.com/v2/account/keys"
```

### List available SSH Keys

request a list of ssh keys

```bash
curl -X GET \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TF_VAR_do_api_token" \
  "https://api.digitalocean.com/v2/account/keys"
```

response includes

```json
{
  "ssh_keys":[
    {
      "id":9246644,
      "fingerprint":"e1:bc:85:3f:2a:62:04:3b:ea:fe:6f:6d:5e:04:ea:65",
      "public_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC4QCqtj...",
      "name":"russell.t.sherman@gmail.com"
    }
  ],
  "links":{},
  "meta":{"total":1}
}
```

response includes keys and details

### Destroy SSH key

```bash
curl -X DELETE \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TF_VAR_do_api_token" \
  "https://api.digitalocean.com/v2/account/keys/9246644"
