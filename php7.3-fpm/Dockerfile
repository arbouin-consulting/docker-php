FROM php:7.3-fpm

RUN apt-get update \
    && apt-get install --no-install-recommends -yqq \
        vim \
        libicu-dev \
        libcurl4-openssl-dev \
        zlib1g-dev \
        git git-core \
        gcc make autoconf libc-dev pkg-config \
        zlib1g-dev \
        curl \
        zsh \
        wget \
        python \
        python-pip \
        unzip \
        libpng-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libxrender1 \
        libfontconfig \
        libxtst6 \
        xz-utils \
        libzip-dev \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && curl "https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz" -L -o "wkhtmltopdf.tar.xz" \
    && tar Jxvf wkhtmltopdf.tar.xz \
    && mv wkhtmltox/bin/wkhtmltopdf /usr/local/bin/wkhtmltopdf \
    && rm -rf wkhtmltopdf.tar.xz wkhtmltox/ \
    && docker-php-ext-install \
        opcache \
        intl \
        mbstring \
        pdo_mysql \
        zip \
        json \
        curl \
        sockets \
        bcmath \
        gd \
    && pecl install xdebug mongodb \
    && echo "extension=mongodb.so" >> /usr/local/etc/php/conf.d/mongodb.ini \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer \
    && apt-get clean \
    && rm -rf /root/.composer/cache/* \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && bash -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" \
    && sed -i -- 's/robbyrussell/wezm+/g' /root/.zshrc \
    && echo "source /root/.oh-my-zsh/oh-my-zsh.sh" >> ~/.zshrc \
    && sed -i -- 's/git/git git-flow git-extras symfony2 command-not-found composer/g' ~/.zshrc \
    && echo 'export PATH=$HOME/bin:/usr/local/bin:/usr/local/sbin:$HOME/.composer/vendor/bin:$PATH' >> ~/.bashrc \
    && echo 'export PATH=$HOME/bin:/usr/local/bin:/usr/local/sbin:$HOME/.composer/vendor/bin:$PATH' >> ~/.zshrc \
    && echo "alias sf='bin/console'" >> ~/.bashrc \
    && echo "alias ls='ls --color'" >> ~/.bashrc \
    && echo "alias ll='ls -l'" >> ~/.bashrc \
    && echo "alias la='ls -la'" >> ~/.bashrc \
    && apt-get remove -y \
        wget \
        git git-core \
        vim \
        python \
        python-pip \
    && apt-get clean \
    && rm -rf /root/.composer/cache/* \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV TERM=xterm
