// Create first nginx server to manage the nodeapp from 1 to 5
docker run --hostname testng1 --name testng1 -p 90:8080 -v ${pwd}/nginx.conf:/etc/nginx/nginx.conf -d nginx
// Create first nginx server to manage the nodeapp from 6 to 10
docker run --hostname testng2 --name testng2 -p 91:8080 -v ${pwd}/nginx1.conf:/etc/nginx/nginx.conf -d nginx

// With the existence of nodeapp image, reuse that image to create nodeapp 1 - 10
docker run --hostname testnodeapp(1-10) --name testnodeapp(1-10) -d nodeapp

// Create a new docker network
docker create network testbackendnet

// Add all containers to new docker network
docker network connect testbackendnet testnodeapp(1-10)
docker network connect testbackendnet testng1
docker network connect testbackendnet testng2


