FROM centos:6.8

ENV NGINX_VERSION 1.14.0

RUN rm -rf /etc/yum.repos.d/* \
	&& curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo \
	&& yum clean all && yum makecache \
	&& yum install zlib-devel pcre-devel make gcc libc-devel openssl openssl-devel curl perl-devel geoip-devel gd-devel libxslt-devel gnupg linux-headers -y 

RUN useradd -d /var/cache/nginx -c "Nginx Server User" -s /sbin/nologin nginx 

RUN curl -fSL https://nginx.org/download/nginx-$NGINX_VERSION.tar.gz -o nginx-$NGINX_VERSION.tar.gz

RUN tar xzf nginx-$NGINX_VERSION.tar.gz && cd nginx-$NGINX_VERSION && ./configure \
		--prefix=/usr/local/nginx \
		--user=nginx \
		--group=nginx \
		--with-http_ssl_module \
		--with-http_realip_module \
		--with-http_addition_module \
		--with-http_sub_module \
		--with-http_dav_module \
		--with-http_flv_module \
		--with-http_mp4_module \
		--with-http_gunzip_module \
		--with-http_gzip_static_module \
		--with-http_random_index_module \
		--with-http_secure_link_module \
		--with-http_stub_status_module \
		--with-http_auth_request_module \
		--with-http_xslt_module=dynamic \
		--with-http_image_filter_module=dynamic \
		--with-stream \
		--with-stream_ssl_module \
		--with-stream_ssl_preread_module \
		--with-stream_realip_module \
		--with-http_slice_module \
		--with-mail \
		--with-mail_ssl_module \
		--with-compat \
		--with-file-aio \
		--with-http_v2_module \
	&& make && make install

RUN ln -s /usr/local/nginx/sbin/* /usr/local/sbin/ && rm -rf ./nginx*

EXPOSE 80 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
