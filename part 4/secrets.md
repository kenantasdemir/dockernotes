<b><mark>docker secret create username .\username.txt</mark></b><br>
//username.txt adlı dosyanın içeriğini username secret nesnesine atar.<br>


echo "bu bir denemedir." | docker secret create denemesecret

docker exec -it containerID sh
/run/secrets altında secret nesneleri saklanır.


<b><mark>docker service create -d --name secretdeneme --secret username --secret sifre kenant42/app1</mark></b><br>

<b><mark>echo "sifrelenecekmetin" | docker secret create sifre2 -</mark></b><br><br>
<b><mark>docker service update --secret-rm sifre --secret-add sifre2 secretdeneme</mark></b><br>
