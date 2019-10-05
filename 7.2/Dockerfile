FROM centos/php-72-centos7

# This image provides an PHP-FPM environment for running PHP
# applications.

EXPOSE 9000

# Description
# This image provides an PHP 7.2 environment for running PHP applications.
# Exposed ports:
# * 9000 - FastCGI Port

ENV PHP_VERSION=7.2 \
    PHP_VER_SHORT=72 \
    NAME=php \
    PATH=$PATH:/opt/rh/rh-php72/root/usr/sbin

ENV SUMMARY="Platform for building and running PHP $PHP_VERSION applications" \
    DESCRIPTION="PHP $PHP_VERSION available as container is a base platform for \
building and running various PHP $PHP_VERSION applications and frameworks. \
PHP is an HTML-embedded scripting language. PHP attempts to make it easy for developers \
to write dynamically generated web pages. PHP also offers built-in database integration \
for several commercial and non-commercial database management systems, so writing \
a database-enabled webpage with PHP is fairly simple. The most common use of PHP coding \
is probably as a replacement for CGI scripts."

LABEL summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.description="${DESCRIPTION}" \
      io.k8s.display-name="PHP-FPM ${PHP_VERSION}" \
      io.openshift.expose-services="9000:fastcgi" \
      io.openshift.tags="${NAME},${NAME}${PHP_VER_SHORT},rh-${NAME}${PHP_VER_SHORT}" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.s2i.scripts-url="image:///usr/libexec/s2i" \
      name="bpserduto/${NAME}-${PHP_VER_SHORT}-fpm-centos7" \
      version="${PHP_VERSION}" 

# Copy extra files to the image.
COPY ./root/ /

# Erase Apache Install PHP-FPM
RUN yum shell /tmp/yumcmd.txt

# Reset permissions of filesystem to default values
RUN /usr/libexec/container-setup && rpm-file-permissions

USER 1001

# Set the default CMD to print the usage of the language image
CMD $STI_SCRIPTS_PATH/usage
