# Install 

cd wordpress-docker

cp env.config .env

docker-compose build

# Install by CLI
docker-compose run --rm wpcli wp core install --url=your_domain --title=Your_Blog_Title --admin_user=username --admin_password=password --admin_email=your_email.com

# Backup DB
docker exec -it wordpress-docker_db_1 mysqldump -u root -proot wordpress > zaloha.sql

# Restore DB
cat zaloha.sql | docker exec -i wordpress-docker_db_1 mysql -u root -proot wordpress

# Backup file system
tar cvfz wordpress.tar.gz build/wordpress

# Restore file system
tar xvfz wordpress.tar.gz -C build/wordpress

# Change URL by CLI
docker-compose run --rm wpcli wp search-replace [OLD_URL] [NEW_URL] --all-tables


