# Magento2 dockerized development environemt

Based on ["Docker for Magento 2 Development" article](https://www.magemodule.com/all-things-magento/magento-2-tutorials/docker-magento-2-development/)

## Steps to spin up docker containers
1. Clone this repository
2. Clone magento2 
    ```
    git clone git@github.com:magento/magento2.git src/magento2ce
    ```
3. Checkout magento from `2.2.9` tag
    ```
    git -C "src/magento2ce" checkout 2.2.9
    ```
4. Spin up containers 
    ```
    docker-compose up -d --build
    ```
5. Run `bash` session inside the `web` containter
    ```
    docker exec -it web bash
    ```
6. Install magento
    ```
    HOST_NAME="m2.local" && \
    cd /app && \
    composer install && \
    bin/magento setup:install \
        --admin-firstname=First \
        --admin-lastname=Last \
        --admin-email="dmitry.smolovich@icfnext.com" \
        --admin-user=admin \
        --admin-password=DemoPassword0 \
        --base-url=https://"$HOST_NAME" \
        --base-url-secure=https://"$HOST_NAME" \
        --backend-frontname=admin \
        --db-host=mysql \
        --db-name=magento \
        --db-user=root \
        --db-password=root \
        --use-rewrites=1 \
        --language=en_CA \
        --currency=CAD \
        --timezone=America/Toronto \
        --use-secure-admin=1 \
        --admin-use-security-key=1 \
        --session-save=files \
        --cache-backend=redis \
        --cache-backend-redis-server=redis \
        --cache-backend-redis-db=0 \
        --page-cache=redis \
        --page-cache-redis-server=redis \
        --page-cache-redis-db=1 && \
    bin/magento deploy:mode:set developer && \
    exit
    ```
7. Add `m2.local` hostname to your `/etc/hosts` file
    ```
    sudo echo '127.0.0.1 m2.local' >> /etc/hosts
    ```
8. Open [m2.local](https://m2.local/) in your browser