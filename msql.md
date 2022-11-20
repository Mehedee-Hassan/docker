 docker-compose.yml                                                                                                                                                                                                      
 version: '3.3'
 services:
   db:
     image: mysql:5.7
       #restart: always
     environment:
       MYSQL_DATABASE: 'test'
       # So you don't have to use root, but you can if you like
       # MYSQL_USER: 'root'
       # You can use whatever password you like
       MYSQL_PASSWORD: 'root'
       # Password for root access
       MYSQL_ROOT_PASSWORD: 'root'
     ports:
       # <Port exposed> : < MySQL Port running inside container>
       - '3307:3306'
     expose:
       # Opens port 3306 on the container
       - '3306'
       # Where our data will be persisted
     volumes:
       - my-db:/file_path/mysql1
 # Names our volume
 volumes:
   my-db:

  
  
  -- commands --
  docker-compose up
  sudo docker exec -it read_replica-db-1 bash
  
  
  docker exec -i read_replica-db-1 sh -c 'exec mysql -uroot -proot test' < /home/mhr/Documents/programming/datageneration/transaction_data/data/*.sql
                                                                                                                                                     
  -- data population ---
                                                                                                                                                     
 #!/bin/bash
 LIST=$(ls -rt '/home/mhr/Documents/programming/datageneration/transaction_data/data0') # THIS LINE CHANGED
 
 for i in $LIST; do # THIS LINE CHANGED
 
     echo $i
     docker exec -i read_replica-db-1 sh -c 'exec mysql -uroot -proot test' < '/home/mhr/Documents/programming/datageneration/transaction_data/data0/'$i
     #mysql --user=<user> --password=<passwd> <database> < $i
 
 done
                                                                            
 #/home/mhr/Documents/programming/datageneration/transaction_data/data0
                                                                                                                                                     
                                                                                                                                                     
