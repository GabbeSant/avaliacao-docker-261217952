# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Gabriel Santoni Espindola
Matrícula: 261217952
Usuário do GitHub: GabbeSant
Usuário do Docker Hub: gabesant

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?
R: Utilizei a imagem base nginx:1.27-alpine conforme a documentação e o tamanho da imagem é 21 MB.
2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.
R:  O Nginx procura os arquivos do site em `/usr/share/nginx/html` (COPY html/ /usr/share/nginx/html/)
Usei o comando:
`docker exec teste-portal ls -l /usr/share/nginx/html`
A saída confirmou que o arquivo `index.html` está presente nesse diretório.
"PS C:\Users\Aluno\Downloads\01.A - Projeto_Avaliação\01.1 - Projeto_Avaliação\avaliacao-docker-agrovale> docker exec teste-portal ls -l /usr/share/nginx/html
total 12
-rw-r--r--    1 root     root           497 Apr 16  2025 50x.html
-rwxr-xr-x    1 root     root          1297 Oct  5 23:34 estilo.css
-rwxr-xr-x    1 root     root          2277 Oct  5 23:52 index.html
"

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
Repo: gabesant/agrovale-portal
Tag: 1.0-261217952
Nome completo da imagem: gabesant/agrovale-portal:1.0-261217952
Link do Repo: https://hub.docker.com/r/gabesant/agrovale-portal

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?
R: Porque o token de acesso é mais seguro do que utilizar diretamente a senha da conta. 

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | COPY | O arquivo `site/index.html` não estava sendo copiado para a imagem. | O container iniciou normalmente, mas apareceu a página padrão "Welcome to nginx!". | Adicionei uma instrução `COPY` para copiar a página de manutenção para o diretório servido pelo Nginx. |
| 2 | WORKDIR/COPY | O arquivo foi copiado para `/usr/share/nginx`, mas o Nginx serve o conteúdo de `/usr/share/nginx/html`. | Mesmo após adicionar o `COPY`, continuou aparecendo a página padrão do Nginx. | Corrigi o diretório de destino para `/usr/share/nginx/html`. |
| 3 | EXPOSE | A porta 80 não estava documentada explicitamente no Dockerfile. | O container funcionou porque a imagem base do Nginx já expõe a porta 80, então não houve erro visível na execução. | Adicionei `EXPOSE 80` para deixar a porta do serviço declarada explicitamente no Dockerfile. |
6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?
R: A opção `-p` segue o formato `porta_do_host:porta_do_container`. Em `-p 7042:80`, a porta 7042 é a porta acessada no computador e a porta 80 é a porta dentro do container.Em `-p 80:7042`, a porta 80 seria a porta do computador e a 7042 seria a porta interna do container. A porta do container, no caso do Nginx, é a porta 80.

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?
No serviço `blog`, `WORDPRESS_DB_HOST` recebe `db` porque, dentro da rede do Docker Compose, os serviços se comunicam pelo nome do serviço. Se fosse usado `localhost`, o WordPress tentaria acessar o banco dentro do próprio container do blog, e não no container `db`.

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.
O serviço `db` não publica a porta 3306 porque o banco só precisa ser acessado internamente pelos containers da mesma rede do Docker Compose, evitando expor o MariaDB no host.
Para consultar o banco sem publicar a porta, usei:
`docker compose exec db mariadb -u root -p`
O comando abriu o cliente MariaDB dentro do container do serviço `db`.
"PS C:\Users\Aluno\Downloads\01.A - Projeto_Avaliação\01.1 - Projeto_Avaliação\avaliacao-docker-agrovale> docker compose exec db mariadb -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 12
Server version: 11.4.13-MariaDB-ubu2404 mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> exit
Bye"
## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
