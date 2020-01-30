FROM nextcloud:fpm-alpine
ENV USER_ID_AFTER=788 GROUP_ID_AFTER=788 WWW_DATA_UID=33 WWW_DATA_GID=33
RUN set -x \
&& apk add --no-cache shadow \
&& USER_NAME_BEFORE=$(grep "^[^:]*:[^:]*:${WWW_DATA_UID}:" /etc/passwd | cut -d : -f 1) \
&& GROUP_NAME_BEFORE=$(grep "^[^:]*:[^:]*:${WWW_DATA_GID}:" /etc/group | cut -d : -f 1) \
&& WWW_DATA_UID_BEFORE=$(grep '^www-data:' /etc/passwd | cut -d : -f 3) \
&& WWW_DATA_GID_BEFORE=$(grep '^www-data:' /etc/group | cut -d : -f 3) \
&& usermod  -u $USER_ID_AFTER $USER_NAME_BEFORE \
&& groupmod -g $GROUP_ID_AFTER $GROUP_NAME_BEFORE \
&& find / -group $WWW_DATA_GID -exec chgrp -h $GROUP_ID_AFTER {} \; \
&& find / -user  $WWW_DATA_UID -exec chown -h $USER_ID_AFTER {} \; \
&& usermod  -u $WWW_DATA_UID www-data \
&& groupmod -g $WWW_DATA_GID www-data \
&& find / -group $WWW_DATA_GID_BEFORE -exec chgrp -h $WWW_DATA_GID {} \; \
&& find / -user  $WWW_DATA_UID_BEFORE -exec chown -h $WWW_DATA_UID {} \; \
&& apk del shadow \
&& mkdir /var/cache/nginx \
&& chown $WWW_DATA_UID /var/cache/nginx \
&& chgrp $WWW_DATA_GID /var/cache/nginx
