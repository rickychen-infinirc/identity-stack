## identity-stack

# 建立一個網絡，讓容器之間可以通信
docker network create ldap-network

# 啟動 OpenLDAP 容器
docker run -p 389:389 -p 636:636 --name openldap \
  --network ldap-network \
  --hostname openldap \
  -e LDAP_ORGANISATION="My Company" \
  -e LDAP_DOMAIN="ldap.infinirc.com" \
  -e LDAP_ADMIN_PASSWORD="admin" \
  -e LDAP_TLS=false \
  --detach osixia/openldap:latest



  # 啟動 phpLDAPadmin 容器
docker run -p 8080:80 --name phpldapadmin \
  --network ldap-network \
  -e PHPLDAPADMIN_LDAP_HOSTS=openldap \
  -e PHPLDAPADMIN_HTTPS=false \
  --detach osixia/phpldapadmin:latest



帳號：cn=admin,dc=ldap,dc=infinirc,dc=com
密碼：admin
