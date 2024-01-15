# certbot-aliyun-dns
自动颁发域名使用阿里云DNS添加TXT验证

### 目前因为云厂商开始对免费的SSL证书，有效期改为3个月了。故在测试过程中需要经常替换证书

> certbot 仅支持国外的云厂商DNS-TXT验证

### 申请证书
``` shell
docker run -it --rm \
  -v $(pwd)/cert:/etc/letsencrypt \
  -v $(pwd)/var:/var/lib/letsencrypt \
  -v $(pwd)/log:/var/log/letsencrypt \
  -v $(pwd)/script:/opt/script \
  -e ACCESS_KEY_ID="" \
  -e ACCESS_KEY_SRCRET="" \
  registry.cn-shanghai.aliyuncs.com/yk-base/certbot-aliyun-dns certonly \
  --manual --preferred-challenges dns \
  --manual-auth-hook /opt/script/auth_hook_script.sh \
  --manual-cleanup-hook /opt/script/cleanup_hook_script.sh \
  -d "domain.com,*.domain.com"
```

### 证书续期
``` shell
docker run -it --rm \
  -v $(pwd)/cert:/etc/letsencrypt \
  -v $(pwd)/var:/var/lib/letsencrypt \
  -v $(pwd)/log:/var/log/letsencrypt \
  -v $(pwd)/script:/opt/script \
  -e ACCESS_KEY_ID="" \
  -e ACCESS_KEY_SRCRET="" \
  registry.cn-shanghai.aliyuncs.com/yk-base/certbot-aliyun-dns renew
```