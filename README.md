# Practica-2---Montar-volumes-en-apache
## Requisitos
1. Asegurarse de que a imaxe `httpd` está dispoñible en Docker.
2. Crear un contedor principal (`asir_httpd`) e configurar o mapeo de portos e o bind mount.
3. Crear dous contedores adicionais (`asir_web1` e `asir_web2`) que compartan o mesmo directorio
`htdocs` pero usen portos distintos.
4. Verificar a visualización da páxina HTML en todos os contedores.
Pasos
1. Comprobar que temos a imaxe `httpd`
docker images | grep httpd
Se non está, descargámola:
docker pull httpd
2. Crear o contedor `asir_httpd`
docker run -d --name asir_httpd -p 8080:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd
Explicación:
- `-d`: Executa o contedor en segundo plano.
- `--name asir_httpd`: Asigna o nome `asir_httpd` ao contedor.
- `-p 8080:80`: Mapea o porto 80 do contedor ao porto 8080 do sistema.
- `-v "$PWD"/htdocs:/usr/local/apache2/htdocs/`: Usa `bind mount` para compartir o directorio
`htdocs` do contedor.
3. Crear unha páxina HTML para probar
Engadimos este HTML no directorio `htdocs/index.html`:
```
<!DOCTYPE html>
<html lang="gl">
<head><meta charset="UTF-8"><title>Benvido a ASIR</title></head>
<body><h1>Este é o servidor Apache de ASIR!</h1></body>
</html>
```
4. Acceder á páxina desde o navegador
Abrimos un navegador e imos a `http://localhost:8080` para ver a páxina de benvida.
5. Crear contedores adicionais `asir_web1` e `asir_web2`
Crear `asir_web1` no porto 8000:
docker run -d --name asir_web1 -p 8000:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd
Crear `asir_web2` no porto 8090:
docker run -d --name asir_web2 -p 8090:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd
6. Comprobar que ambos servidores mostran a mesma páxina
Verificamos que `http://localhost:8000` e `http://localhost:8090` mostran a mesma páxina.
Entrega
Este README e o código están dispoñibles en [este repositorio de
GitHub](https://github.com/J0aka/Practica-1-Comandos-de-docker).
