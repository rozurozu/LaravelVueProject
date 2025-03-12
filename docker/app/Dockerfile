FROM php:8.2-fpm

# システムの依存関係インストール
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

# PHPの拡張機能インストール
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Composerのインストール
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 作業ディレクトリの設定
WORKDIR /var/www

# ユーザー権限設定
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# PHPの設定ファイルをコピー
COPY php.ini /usr/local/etc/php/

# 所有権変更
RUN chown -R www:www /var/www

# ユーザー切り替え
USER www

# コンテナ起動時のコマンド
CMD ["php-fpm"]

EXPOSE 9000
