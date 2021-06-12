### Getting started with docker-compose laravel environment


#### installing dependencies 

* docker 

Follow download instructions from [official site](https://docs.docker.com/get-docker/).

*  curl jq (skip for windows/mac)

```sh
sudo apt install curl jq 
```

* docker-compose (skip for windows/mac)

```sh
curl --silent "https://api.github.com/repos/docker/compose/releases/latest" | jq --arg PLATFORM_ARCH "$(echo `uname -s`-`uname -m`)" -r '.assets[] | select(.name | endswith($PLATFORM_ARCH)).browser_download_url' | xargs sudo curl -L -o /usr/local/bin/docker-compose --url

```

_For **Windows & macOS** Docker Compose is included in Docker Desktop._

### Steps for using the docker-compose environment

* Copy docker-compose.yaml file to your project's root dir

* Copy nginx-default.conf file to your project's root dir

* Edit both files according to your requirements (e.g. php verison, composer version mysql password, listening ports for app/phpmyadmin)

* Open terminal in the directory where above files are copied to and run command
```sh
mkdir ~/mysql-data
```
```sh
docker compose up -d
```

###### & your application is live, open up http://localhost:8080 on your favourite browser to visit your laravel app &nbsp;

### Default ports for applications

| &nbsp; &nbsp; &nbsp; &nbsp;Application  &nbsp; &nbsp; &nbsp; &nbsp; | &nbsp; &nbsp; &nbsp; &nbsp; Port &nbsp; &nbsp; &nbsp; &nbsp; |
| ------------- |:-------------:|
| &nbsp; &nbsp; &nbsp; &nbsp;laravel     |  **8080**  |
| &nbsp; &nbsp; &nbsp; &nbsp;phpmyadmin | **8888** |
| &nbsp; &nbsp; &nbsp; &nbsp;mysql | **3307** |

_Use port **3307** for **mysql-server** if you're using a **desktop client** such as **workbench** or **sequel pro/table plus**._
##### Default creds for phpmyadmin/mysql

`root` : `laravel`

#### laravel env vars 
```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=laravel

REDIS_HOST=redis 
```


### various commands for interacting with environment

| Command  | Use case |
| ------------- |:-------------:|
| docker-compose run --rm npm install     | if npm is not installed on local   |
| docker-compose run --rm composer install | if composer is not installed on local |
| docker-compose run --rm artisan config:clear | if php is not installed on local|

### the docker-compose run command alias

add the below line at the end of your shell's rc file 

e.g `~/.bahsrc` if your shell is **bash** `~/.zshrc` if your shell is **zsh**

```sh
alias dr="docker-compose run --rm"
```

### after alias installation these commands will be

| Command  | Use case |
| ------------- |:-------------:|
| dr npm install     | if npm is not installed on local   |
| dr composer install | if composer is not installed on local |
| dr artisan config:clear | if php is not installed on local|

### for shutting down the containers
open a terminal in project's root directory & run

```sh
docker-compose down
```