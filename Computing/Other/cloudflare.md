## Dynamically update cloudlfare records

(record has to already exist)

crontab

```
0 */6 * * * /usr/local/sbin/updateCF.sh -z ryanl.co.uk -d ryanl.co.uk >> /var/log/updateCF.log
05 */6 * * * /usr/local/sbin/updateCF.sh -z ryanl.co.uk -d cloud.ryanl.co.uk >> /var/log/updateCF.log

10 */6 * * * /usr/local/sbin/updateCF.sh -z 2kanna.org -d 2kanna.org >> /var/log/updateCF.log
```

/usr/local/sbin/updateCF.sh

```
dt=$(date '+%d/%m/%Y %H:%M:%S');
echo "========== $dt =========="

while getopts z:d: flag
do
    case "${flag}" in
        z) zone=${OPTARG};;
        d) dnsrecord=${OPTARG};;
    esac
done

## Cloudflare authentication details
## keep these private
cloudflare_auth_email=ryan.linnit@outlook.com
cloudflare_auth_key=CHANGE


# Get the current external IP address
ip=$(curl -s -X GET https://checkip.amazonaws.com)

echo "Current IP is $ip"

if host $dnsrecord 1.1.1.1 | grep "has address" | grep "$ip"; then
  echo "$dnsrecord is currently set to $ip; no changes needed"
  echo "========================================="
  exit
fi

# if here, the dns record needs updating

# get the zone id for the requested zone
zoneid=$(curl -s -X GET "https://api.cloudflare.com/client/v4/zones?name=$zone&status=active" \
  -H "X-Auth-Email: $cloudflare_auth_email" \
  -H "Authorization: Bearer $cloudflare_auth_key" \
  -H "Content-Type: application/json" | jq -r '{"result"}[] | .[0] | .id')

echo "Zoneid for $zone is $zoneid"

# get the dns record id
dnsrecordid=$(curl -s -X GET "https://api.cloudflare.com/client/v4/zones/$zoneid/dns_records?type=A&name=$dnsrecord" \
  -H "X-Auth-Email: $cloudflare_auth_email" \
  -H "Authorization: Bearer $cloudflare_auth_key" \
  -H "Content-Type: application/json" | jq -r '{"result"}[] | .[0] | .id')

echo "DNSrecordid for $dnsrecord is $dnsrecordid"

# update the record
curl -s -X PUT "https://api.cloudflare.com/client/v4/zones/$zoneid/dns_records/$dnsrecordid" \
  -H "X-Auth-Email: $cloudflare_auth_email" \
  -H "Authorization: Bearer $cloudflare_auth_key" \
  -H "Content-Type: application/json" \ 
  --data "{\"type\":\"A\",\"name\":\"$dnsrecord\",\"content\":\"$ip\",\"ttl\":1,\"proxied\":false}" | jq

echo "========================================="
```