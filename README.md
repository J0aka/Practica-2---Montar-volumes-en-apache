
### Paso 1: Comproba a imaxe `httpd`
Executa o seguinte comando para verificar se a imaxe `httpd` está dispoñible:
```bash
docker images | grep httpd
```
Se a imaxe non está, descarga con:
```bash
docker pull httpd
```
### Paso 2: Crea o directorio `htdocs`
No teu directorio de traballo, crea o directorio `htdocs`:
```bash
mkdir -p /home/J0aka/htdocs
```
Engade un ficheiro `index.html` co contido:
```bash
echo "<h1>Ola desde Apache</h1>" > /home/J0aka/htdocs/index.html
```
### Paso 3: Crea o contedor `asir_httpd`
Mapea o porto 80 do contedor ao 8080 da máquina host e usa `bind mount`:
```bash
docker run -d --name asir_httpd -p 8080:80 -v /home/J0aka/htdocs:/usr/local/apache2/htdocs/ httpd
```
### Paso 4: Comproba `asir_httpd`
Abre `http://localhost:8080` no navegador para ver `index.html`.
### Paso 5: Crea `asir_web1` co porto 8000
```bash
docker run -d --name asir_web1 -p 8000:80 -v /home/J0aka/htdocs:/usr/local/apache2/htdocs/ httpd
```
### Paso 6: Crea `asir_web2` co porto 8090
```bash
docker run -d --name asir_web2 -p 8090:80 -v /home/J0aka/htdocs:/usr/local/apache2/htdocs/ httpd
```
### Paso 7: Comproba ambos contedores
Abre `http://localhost:8000` e `http://localhost:8090` para ver a páxina compartida.
---
