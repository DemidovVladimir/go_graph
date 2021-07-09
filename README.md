### Generate resolvers based on the graph model:
go run github.com/99designs/gqlgen generate 

### Run MySQL single replica:
docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=dbpass -e MYSQL_DATABASE=hackernews -d mysql:latest

### Install db migratin tool:
go build -tags 'mysql' -ldflags="-X main.Version=1.0.0" -o $GOPATH/bin/migrate github.com/golang-migrate/migrate/v4/cmd/migrate/

###  Create user table by using migration tool:
migrate create -ext sql -dir mysql -seq create_users_table

### Create links table by using  migration tool:
migrate create -ext sql -dir mysql -seq create_links_table

### Finaly run the server:
go run server.go