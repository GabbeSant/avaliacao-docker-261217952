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

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
