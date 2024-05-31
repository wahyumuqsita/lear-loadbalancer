# Learn Loadbalancer

## 1. Create Container as Loadbalancer Upstream

Run these command : 
```bash
$ for i in {1,2,3};do sudo docker run -p 500$i:5000 -d --name api-auth-$i wahyumw/simple-api:auth; done
$ for i in {1,2,3};do sudo docker run -p 600$i:5000 -d --name api-user-$i wahyumw/simple-api:user; done
$ for i in {1,2,3};do sudo docker run -p 700$i:5000 -d --name api-transaction-$i wahyumw/simple-api:transaction; done
```

## 2. Configure nginx

1. Copy nginx configuration
```bash
sudo cp ./api.conf /etc/nginx/sites-enabled/api.conf
```
2. Test configuration 
```bash
sudo nginx -t
```
3. Reload configuration 
```bash
sudo nginx -s reload
```

## 3. Test The Loadbalancer

1. Test using curl
```bash
$ curl localhost/user -H "Host: api.example.com"
$ curl localhost/auth -H "Host: api.example.com"
$ curl localhost/transaction -H "Host: api.example.com"
```
2. Check access log
```bash
sudo tail -10 /var/log/nginx/access-api.log
```